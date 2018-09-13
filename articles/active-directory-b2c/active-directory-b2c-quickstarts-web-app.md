---
title: Quickstart - Set up sign-in for an ASP.NET application using Azure Active Directory B2C | Microsoft Docs
description: Run a sample ASP.NET web app that uses Azure Active Directory B2C to provide account sign-in.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.topic: quickstart
ms.custom: mvc
ms.date: 2/13/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: e52674014a888913e288f7b0749d9b2e05bedf45
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857394"
---
# <a name="quickstart-set-up-sign-in-for-an-aspnet-application-using-azure-active-directory-b2c"></a><span data-ttu-id="bb12d-103">Quickstart: Set up sign-in for an ASP.NET application using Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="bb12d-103">Quickstart: Set up sign-in for an ASP.NET application using Azure Active Directory B2C</span></span>

<span data-ttu-id="bb12d-104">Azure Active Directory (Azure AD) B2C provides cloud identity management to keep your application, business, and customers protected.</span><span class="sxs-lookup"><span data-stu-id="bb12d-104">Azure Active Directory (Azure AD) B2C provides cloud identity management to keep your application, business, and customers protected.</span></span> <span data-ttu-id="bb12d-105">Azure AD B2C enables your apps to authenticate to social accounts, and enterprise accounts using open standard protocols.</span><span class="sxs-lookup"><span data-stu-id="bb12d-105">Azure AD B2C enables your apps to authenticate to social accounts, and enterprise accounts using open standard protocols.</span></span>

<span data-ttu-id="bb12d-106">In this quickstart, you use an Azure AD B2C enabled sample ASP.NET app to sign in using a social identity provider and call an Azure AD B2C protected web API.</span><span class="sxs-lookup"><span data-stu-id="bb12d-106">In this quickstart, you use an Azure AD B2C enabled sample ASP.NET app to sign in using a social identity provider and call an Azure AD B2C protected web API.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="bb12d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb12d-107">Prerequisites</span></span>

* <span data-ttu-id="bb12d-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="bb12d-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **ASP.NET and web development** workload.</span></span> 
* <span data-ttu-id="bb12d-109">A social account from either Facebook, Google, Microsoft, or Twitter.</span><span class="sxs-lookup"><span data-stu-id="bb12d-109">A social account from either Facebook, Google, Microsoft, or Twitter.</span></span>

## <a name="download-the-sample"></a><span data-ttu-id="bb12d-110">Download the sample</span><span class="sxs-lookup"><span data-stu-id="bb12d-110">Download the sample</span></span>

<span data-ttu-id="bb12d-111">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi/archive/master.zip) or clone the sample web app from GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb12d-111">[Download a zip file](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi/archive/master.zip) or clone the sample web app from GitHub.</span></span>

```
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

## <a name="run-the-app-in-visual-studio"></a><span data-ttu-id="bb12d-112">Run the app in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb12d-112">Run the app in Visual Studio</span></span>

<span data-ttu-id="bb12d-113">In the sample application project folder, open the `B2C-WebAPI-DotNet.sln` solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb12d-113">In the sample application project folder, open the `B2C-WebAPI-DotNet.sln` solution in Visual Studio.</span></span>

<span data-ttu-id="bb12d-114">There are two projects in the sample solution:</span><span class="sxs-lookup"><span data-stu-id="bb12d-114">There are two projects in the sample solution:</span></span>

<span data-ttu-id="bb12d-115">**Web app sample app (TaskWebApp):** Web app to create and edit a task list.</span><span class="sxs-lookup"><span data-stu-id="bb12d-115">**Web app sample app (TaskWebApp):** Web app to create and edit a task list.</span></span> <span data-ttu-id="bb12d-116">The web app uses the **sign-up or sign-in** policy to sign up or sign in users.</span><span class="sxs-lookup"><span data-stu-id="bb12d-116">The web app uses the **sign-up or sign-in** policy to sign up or sign in users.</span></span>

<span data-ttu-id="bb12d-117">**Web API sample app (TaskService):** Web API that supports the create, read, update, and delete task list functionality.</span><span class="sxs-lookup"><span data-stu-id="bb12d-117">**Web API sample app (TaskService):** Web API that supports the create, read, update, and delete task list functionality.</span></span> <span data-ttu-id="bb12d-118">The web API is protected by Azure AD B2C and called by the web app.</span><span class="sxs-lookup"><span data-stu-id="bb12d-118">The web API is protected by Azure AD B2C and called by the web app.</span></span>

<span data-ttu-id="bb12d-119">For this quickstart, you run both the `TaskWebApp` and `TaskService` projects at the same time.</span><span class="sxs-lookup"><span data-stu-id="bb12d-119">For this quickstart, you run both the `TaskWebApp` and `TaskService` projects at the same time.</span></span> 

1. <span data-ttu-id="bb12d-120">Select solution `B2C-WebAPI-DotNet` in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="bb12d-120">Select solution `B2C-WebAPI-DotNet` in Solution Explorer.</span></span>
2. <span data-ttu-id="bb12d-121">In the Visual Studio menu, select **Project > Set StartUp Projects...**.</span><span class="sxs-lookup"><span data-stu-id="bb12d-121">In the Visual Studio menu, select **Project > Set StartUp Projects...**.</span></span> 
3. <span data-ttu-id="bb12d-122">Select **Multiple startup projects** radio button.</span><span class="sxs-lookup"><span data-stu-id="bb12d-122">Select **Multiple startup projects** radio button.</span></span>
4. <span data-ttu-id="bb12d-123">Change the **Action** for both projects to **Start**.</span><span class="sxs-lookup"><span data-stu-id="bb12d-123">Change the **Action** for both projects to **Start**.</span></span> <span data-ttu-id="bb12d-124">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="bb12d-124">Click **OK**.</span></span>

<span data-ttu-id="bb12d-125">Press **F5** to debug both applications.</span><span class="sxs-lookup"><span data-stu-id="bb12d-125">Press **F5** to debug both applications.</span></span> <span data-ttu-id="bb12d-126">Each application opens in its own browser tab:</span><span class="sxs-lookup"><span data-stu-id="bb12d-126">Each application opens in its own browser tab:</span></span>

<span data-ttu-id="bb12d-127">`https://localhost:44316/` - This page is the ASP.NET web application.</span><span class="sxs-lookup"><span data-stu-id="bb12d-127">`https://localhost:44316/` - This page is the ASP.NET web application.</span></span> <span data-ttu-id="bb12d-128">You interact directly with this application in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="bb12d-128">You interact directly with this application in the quickstart.</span></span>
<span data-ttu-id="bb12d-129">`https://localhost:44332/` - This page is the web API that is called by the ASP.NET web application.</span><span class="sxs-lookup"><span data-stu-id="bb12d-129">`https://localhost:44332/` - This page is the web API that is called by the ASP.NET web application.</span></span>

## <a name="create-an-account"></a><span data-ttu-id="bb12d-130">Create an account</span><span class="sxs-lookup"><span data-stu-id="bb12d-130">Create an account</span></span>

<span data-ttu-id="bb12d-131">Click the **Sign up / Sign in** link in the ASP.NET web application to start the **Sign Up or Sign In** workflow based on an Azure AD B2C policy.</span><span class="sxs-lookup"><span data-stu-id="bb12d-131">Click the **Sign up / Sign in** link in the ASP.NET web application to start the **Sign Up or Sign In** workflow based on an Azure AD B2C policy.</span></span>

![Sample ASP.NET web app](media/active-directory-b2c-quickstarts-web-app/web-app-sign-in.png)

<span data-ttu-id="bb12d-133">The sample supports several sign-up options including using a social identity provider or creating a local account using an email address.</span><span class="sxs-lookup"><span data-stu-id="bb12d-133">The sample supports several sign-up options including using a social identity provider or creating a local account using an email address.</span></span> <span data-ttu-id="bb12d-134">For this quickstart, use a social identity provider account from either Facebook, Google, Microsoft, or Twitter.</span><span class="sxs-lookup"><span data-stu-id="bb12d-134">For this quickstart, use a social identity provider account from either Facebook, Google, Microsoft, or Twitter.</span></span> 

### <a name="sign-up-using-a-social-identity-provider"></a><span data-ttu-id="bb12d-135">Sign up using a social identity provider</span><span class="sxs-lookup"><span data-stu-id="bb12d-135">Sign up using a social identity provider</span></span>

<span data-ttu-id="bb12d-136">Azure AD B2C presents a custom login page for a fictitious brand called Wingtip Toys for the sample web app.</span><span class="sxs-lookup"><span data-stu-id="bb12d-136">Azure AD B2C presents a custom login page for a fictitious brand called Wingtip Toys for the sample web app.</span></span> 

1. <span data-ttu-id="bb12d-137">To sign up using a social identity provider, click the button of the identity provider you want to use.</span><span class="sxs-lookup"><span data-stu-id="bb12d-137">To sign up using a social identity provider, click the button of the identity provider you want to use.</span></span>

    ![Sign In or Sign Up provider](media/active-directory-b2c-quickstarts-web-app/sign-in-or-sign-up-web.png)

    <span data-ttu-id="bb12d-139">You authenticate (sign-in) using your social account credentials and authorize the application to read information from your social account.</span><span class="sxs-lookup"><span data-stu-id="bb12d-139">You authenticate (sign-in) using your social account credentials and authorize the application to read information from your social account.</span></span> <span data-ttu-id="bb12d-140">By granting access, the application can retrieve profile information from the social account such as your name and city.</span><span class="sxs-lookup"><span data-stu-id="bb12d-140">By granting access, the application can retrieve profile information from the social account such as your name and city.</span></span> 

2. <span data-ttu-id="bb12d-141">Finish the sign-in process for the identity provider.</span><span class="sxs-lookup"><span data-stu-id="bb12d-141">Finish the sign-in process for the identity provider.</span></span> <span data-ttu-id="bb12d-142">For example, if you chose Twitter, enter your Twitter credentials and click **Sign in**.</span><span class="sxs-lookup"><span data-stu-id="bb12d-142">For example, if you chose Twitter, enter your Twitter credentials and click **Sign in**.</span></span>

    ![Authenticate and authorize using a social account](media/active-directory-b2c-quickstarts-web-app/twitter-authenticate-authorize-web.png)

    <span data-ttu-id="bb12d-144">Your new Azure AD B2C account profile details are pre-populated with information from your social account.</span><span class="sxs-lookup"><span data-stu-id="bb12d-144">Your new Azure AD B2C account profile details are pre-populated with information from your social account.</span></span>

3. <span data-ttu-id="bb12d-145">Update the Display Name, Job Title, and City fields and click **Continue**.</span><span class="sxs-lookup"><span data-stu-id="bb12d-145">Update the Display Name, Job Title, and City fields and click **Continue**.</span></span>  <span data-ttu-id="bb12d-146">The values you enter are used for your Azure AD B2C user account profile.</span><span class="sxs-lookup"><span data-stu-id="bb12d-146">The values you enter are used for your Azure AD B2C user account profile.</span></span>

    ![New account sign-up profile details](media/active-directory-b2c-quickstarts-web-app/new-account-sign-up-profile-details-web.png)

    <span data-ttu-id="bb12d-148">You have successfully used the sample web app that uses an Azure AD B2C policy to authenticate using an identity provider and create an Azure AD B2C user account.</span><span class="sxs-lookup"><span data-stu-id="bb12d-148">You have successfully used the sample web app that uses an Azure AD B2C policy to authenticate using an identity provider and create an Azure AD B2C user account.</span></span> 

## <a name="edit-your-profile"></a><span data-ttu-id="bb12d-149">Edit your profile</span><span class="sxs-lookup"><span data-stu-id="bb12d-149">Edit your profile</span></span>

<span data-ttu-id="bb12d-150">Azure Active Directory B2C provides functionality to allow users to update their profiles.</span><span class="sxs-lookup"><span data-stu-id="bb12d-150">Azure Active Directory B2C provides functionality to allow users to update their profiles.</span></span> <span data-ttu-id="bb12d-151">The sample web app uses an Azure AD B2C edit profile policy for the workflow.</span><span class="sxs-lookup"><span data-stu-id="bb12d-151">The sample web app uses an Azure AD B2C edit profile policy for the workflow.</span></span> 

1. <span data-ttu-id="bb12d-152">In the web application menu bar, click your profile name and select **Edit profile** to edit the profile you created.</span><span class="sxs-lookup"><span data-stu-id="bb12d-152">In the web application menu bar, click your profile name and select **Edit profile** to edit the profile you created.</span></span>

    ![Edit profile](media/active-directory-b2c-quickstarts-web-app/edit-profile-web.png)

2. <span data-ttu-id="bb12d-154">Change your **Display name** and **City**.</span><span class="sxs-lookup"><span data-stu-id="bb12d-154">Change your **Display name** and **City**.</span></span>  
3. <span data-ttu-id="bb12d-155">Click **Continue** to update your profile.</span><span class="sxs-lookup"><span data-stu-id="bb12d-155">Click **Continue** to update your profile.</span></span> <span data-ttu-id="bb12d-156">The new display name is displayed in the upper right portion of the web app's home page.</span><span class="sxs-lookup"><span data-stu-id="bb12d-156">The new display name is displayed in the upper right portion of the web app's home page.</span></span>

## <a name="access-a-protected-web-api-resource"></a><span data-ttu-id="bb12d-157">Access a protected web API resource</span><span class="sxs-lookup"><span data-stu-id="bb12d-157">Access a protected web API resource</span></span>

1. <span data-ttu-id="bb12d-158">Click **To-Do List** to enter and modify your to-do list items.</span><span class="sxs-lookup"><span data-stu-id="bb12d-158">Click **To-Do List** to enter and modify your to-do list items.</span></span> 

2. <span data-ttu-id="bb12d-159">Enter text in the **New Item** text box.</span><span class="sxs-lookup"><span data-stu-id="bb12d-159">Enter text in the **New Item** text box.</span></span> <span data-ttu-id="bb12d-160">Click **Add** to call the Azure AD B2C protected web API that adds a to-do list item.</span><span class="sxs-lookup"><span data-stu-id="bb12d-160">Click **Add** to call the Azure AD B2C protected web API that adds a to-do list item.</span></span>

    ![Add a to-do list item](media/active-directory-b2c-quickstarts-web-app/add-todo-item-web.png)

    <span data-ttu-id="bb12d-162">The ASP.NET web application includes an Azure AD access token in the request to the protected web API resource to perform operations on the user's to-do list items.</span><span class="sxs-lookup"><span data-stu-id="bb12d-162">The ASP.NET web application includes an Azure AD access token in the request to the protected web API resource to perform operations on the user's to-do list items.</span></span>

<span data-ttu-id="bb12d-163">You have successfully used your Azure AD B2C user account to make an authorized call an Azure AD B2C protected web API.</span><span class="sxs-lookup"><span data-stu-id="bb12d-163">You have successfully used your Azure AD B2C user account to make an authorized call an Azure AD B2C protected web API.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bb12d-164">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bb12d-164">Clean up resources</span></span>

<span data-ttu-id="bb12d-165">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C quickstarts or tutorials.</span><span class="sxs-lookup"><span data-stu-id="bb12d-165">You can use your Azure AD B2C tenant if you plan to try other Azure AD B2C quickstarts or tutorials.</span></span> <span data-ttu-id="bb12d-166">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span><span class="sxs-lookup"><span data-stu-id="bb12d-166">When no longer needed, you can [delete your Azure AD B2C tenant](active-directory-b2c-faqs.md#how-do-i-delete-my-azure-ad-b2c-tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb12d-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="bb12d-167">Next steps</span></span>

<span data-ttu-id="bb12d-168">In this quickstart, you used an Azure AD B2C enabled sample ASP.NET app to sign in with a custom login page, sign in with a social identity provider, create an Azure AD B2C account, and call a web API protected by Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bb12d-168">In this quickstart, you used an Azure AD B2C enabled sample ASP.NET app to sign in with a custom login page, sign in with a social identity provider, create an Azure AD B2C account, and call a web API protected by Azure AD B2C.</span></span> 

<span data-ttu-id="bb12d-169">Continue to the tutorial to learn how to configure the sample ASP.NET to use your own Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="bb12d-169">Continue to the tutorial to learn how to configure the sample ASP.NET to use your own Azure AD B2C tenant.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb12d-170">Create an Azure Active Directory B2C tenant in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bb12d-170">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>](tutorial-create-tenant.md)