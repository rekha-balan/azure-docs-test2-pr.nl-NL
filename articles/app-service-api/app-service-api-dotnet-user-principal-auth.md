---
title: User authentication for API Apps in Azure App Service | Microsoft Docs
description: Learn how to protect an API app in Azure App Service by allowing access only to authenticated users.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: ''
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: bdd7fe6d7870fef614c6e63571c065510f68b5fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549419"
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a><span data-ttu-id="f4500-103">User authentication for API Apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4500-103">User authentication for API Apps in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="f4500-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f4500-104">Overview</span></span>
<span data-ttu-id="f4500-105">This article shows how to protect an Azure API app so that only authenticated users can call it.</span><span class="sxs-lookup"><span data-stu-id="f4500-105">This article shows how to protect an Azure API app so that only authenticated users can call it.</span></span> <span data-ttu-id="f4500-106">The article assumes that you have read the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4500-106">The article assumes that you have read the [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span>

<span data-ttu-id="f4500-107">You'll learn:</span><span class="sxs-lookup"><span data-stu-id="f4500-107">You'll learn:</span></span>

* <span data-ttu-id="f4500-108">How to configure an authentication provider, with details for Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f4500-108">How to configure an authentication provider, with details for Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="f4500-109">How to consume a protected API app by using the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span><span class="sxs-lookup"><span data-stu-id="f4500-109">How to consume a protected API app by using the [Active Directory Authentication Library (ADAL) for JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).</span></span>

<span data-ttu-id="f4500-110">The article contains two sections:</span><span class="sxs-lookup"><span data-stu-id="f4500-110">The article contains two sections:</span></span>

* <span data-ttu-id="f4500-111">The [How to configure user authentication in Azure App Service](#authconfig) section explains in general how to configure user authentication for any API app and applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span><span class="sxs-lookup"><span data-stu-id="f4500-111">The [How to configure user authentication in Azure App Service](#authconfig) section explains in general how to configure user authentication for any API app and applies equally to all frameworks supported by App Service, including .NET, Node.js, and Java.</span></span>
* <span data-ttu-id="f4500-112">Starting with the [Continuing the .NET API Apps tutorials](#tutorialstart) section, the article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span><span class="sxs-lookup"><span data-stu-id="f4500-112">Starting with the [Continuing the .NET API Apps tutorials](#tutorialstart) section, the article guides you through configuring a sample application with a .NET back end and an AngularJS front end so that it uses Azure Active Directory for user authentication.</span></span> 

## <a id="authconfig"></a> <span data-ttu-id="f4500-113">How to configure user authentication in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f4500-113">How to configure user authentication in Azure App Service</span></span>
<span data-ttu-id="f4500-114">This section provides general instructions that apply to any API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-114">This section provides general instructions that apply to any API app.</span></span> <span data-ttu-id="f4500-115">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET getting-started tutorials](#tutorialstart).</span><span class="sxs-lookup"><span data-stu-id="f4500-115">For steps specific to the To Do List .NET sample application, go to [Continuing the .NET getting-started tutorials](#tutorialstart).</span></span>

1. <span data-ttu-id="f4500-116">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, find the **Features** section, and then click **Authentication/ Authorization**.</span><span class="sxs-lookup"><span data-stu-id="f4500-116">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you want to protect, find the **Features** section, and then click **Authentication/ Authorization**.</span></span>
   
    ![Azure portal Authentication/Authorization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="f4500-118">In the **Authentication / Authorization** blade, click **On**.</span><span class="sxs-lookup"><span data-stu-id="f4500-118">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="f4500-119">Select one of the options from the **Action to take when request is not authenticated** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f4500-119">Select one of the options from the **Action to take when request is not authenticated** drop-down list.</span></span>
   
   * <span data-ttu-id="f4500-120">If you want only authenticated calls to reach your API app, choose one of the **Log in with ...** options.</span><span class="sxs-lookup"><span data-stu-id="f4500-120">If you want only authenticated calls to reach your API app, choose one of the **Log in with ...** options.</span></span> <span data-ttu-id="f4500-121">This option enables you to protect the API app without writing any code that runs in it.</span><span class="sxs-lookup"><span data-stu-id="f4500-121">This option enables you to protect the API app without writing any code that runs in it.</span></span>
   * <span data-ttu-id="f4500-122">If you want all calls to reach your API app, choose **Allow request (no action)**.</span><span class="sxs-lookup"><span data-stu-id="f4500-122">If you want all calls to reach your API app, choose **Allow request (no action)**.</span></span> <span data-ttu-id="f4500-123">You can use this option to direct unauthenticated callers to a choice of authentication providers.</span><span class="sxs-lookup"><span data-stu-id="f4500-123">You can use this option to direct unauthenticated callers to a choice of authentication providers.</span></span> <span data-ttu-id="f4500-124">With this option you have to write code to handle authorization.</span><span class="sxs-lookup"><span data-stu-id="f4500-124">With this option you have to write code to handle authorization.</span></span>
     
     <span data-ttu-id="f4500-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span><span class="sxs-lookup"><span data-stu-id="f4500-125">For more information, see [Authentication and authorization for API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options).</span></span>
4. <span data-ttu-id="f4500-126">Select one or more of the **Authentication Providers**.</span><span class="sxs-lookup"><span data-stu-id="f4500-126">Select one or more of the **Authentication Providers**.</span></span>
   
    <span data-ttu-id="f4500-127">The image shows    choices that require all callers to be authenticated by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4500-127">The image shows    choices that require all callers to be authenticated by Azure AD.</span></span>
   
    ![Azure portal Authentication/Authorization blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    <span data-ttu-id="f4500-129">When you choose an authentication provider, the portal displays a configuration blade for that provider.</span><span class="sxs-lookup"><span data-stu-id="f4500-129">When you choose an authentication provider, the portal displays a configuration blade for that provider.</span></span> 
   
    <span data-ttu-id="f4500-130">For detailed instructions that explain how to configure the authentication provider configuration blades, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f4500-130">For detailed instructions that explain how to configure the authentication provider configuration blades, see [How to configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> <span data-ttu-id="f4500-131">(The link goes to an article about Azure AD, but the article itself contains tabs that link to articles for the other authentication providers.)</span><span class="sxs-lookup"><span data-stu-id="f4500-131">(The link goes to an article about Azure AD, but the article itself contains tabs that link to articles for the other authentication providers.)</span></span>
5. <span data-ttu-id="f4500-132">When you're done with the authentication provider configuration blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4500-132">When you're done with the authentication provider configuration blade, click **OK**.</span></span>
6. <span data-ttu-id="f4500-133">In the **Authentication / Authorization** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4500-133">In the **Authentication / Authorization** blade, click **Save**.</span></span>

<span data-ttu-id="f4500-134">When this is done, App Service authenticates all API calls before they reach the API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-134">When this is done, App Service authenticates all API calls before they reach the API app.</span></span> <span data-ttu-id="f4500-135">The authentication services work the same for all languages that App service supports, including .NET, Node.js, and Java.</span><span class="sxs-lookup"><span data-stu-id="f4500-135">The authentication services work the same for all languages that App service supports, including .NET, Node.js, and Java.</span></span> 

<span data-ttu-id="f4500-136">To make authenticated API calls, the caller includes the authentication provider's OAuth 2.0 bearer token in the Authorization header of HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="f4500-136">To make authenticated API calls, the caller includes the authentication provider's OAuth 2.0 bearer token in the Authorization header of HTTP requests.</span></span> <span data-ttu-id="f4500-137">The token can be acquired by using the authentication provider's SDK.</span><span class="sxs-lookup"><span data-stu-id="f4500-137">The token can be acquired by using the authentication provider's SDK.</span></span>

## <a id="tutorialstart"></a> <span data-ttu-id="f4500-138">Continuing the .NET API Apps tutorials</span><span class="sxs-lookup"><span data-stu-id="f4500-138">Continuing the .NET API Apps tutorials</span></span>
<span data-ttu-id="f4500-139">If you are following the Node.js or Java tutorials for API apps, skip to the next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="f4500-139">If you are following the Node.js or Java tutorials for API apps, skip to the next article, [service principal authentication for API apps](app-service-api-dotnet-service-principal-auth.md).</span></span> 

<span data-ttu-id="f4500-140">If you are following the .NET tutorial series for API apps and have already deployed the sample application as directed in the [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip to the [Set up authentication in App Service and Azure AD](#azureauth) section.</span><span class="sxs-lookup"><span data-stu-id="f4500-140">If you are following the .NET tutorial series for API apps and have already deployed the sample application as directed in the [first](app-service-api-dotnet-get-started.md) and [second](app-service-api-cors-consume-javascript.md) tutorials, skip to the [Set up authentication in App Service and Azure AD](#azureauth) section.</span></span>

<span data-ttu-id="f4500-141">If you want to follow this tutorial without going through the first and second tutorials, do the following steps which explain how to get started by using an automated process to deploy the sample application.</span><span class="sxs-lookup"><span data-stu-id="f4500-141">If you want to follow this tutorial without going through the first and second tutorials, do the following steps which explain how to get started by using an automated process to deploy the sample application.</span></span>

> [!NOTE]
> <span data-ttu-id="f4500-142">The following steps get you to the same starting point as if you did the first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span><span class="sxs-lookup"><span data-stu-id="f4500-142">The following steps get you to the same starting point as if you did the first two tutorials, with one exception: Visual Studio won't already know which web app or API app that each project gets deployed to.</span></span> <span data-ttu-id="f4500-143">That means you won't have exact instructions in this tutorial that explain how to deploy to the right targets.</span><span class="sxs-lookup"><span data-stu-id="f4500-143">That means you won't have exact instructions in this tutorial that explain how to deploy to the right targets.</span></span> <span data-ttu-id="f4500-144">If you're not comfortable with figuring out how to do the deployment steps on your own, it's better to follow the tutorial series from the [first tutorial](app-service-api-dotnet-get-started.md) than to start with this automated deployment process.</span><span class="sxs-lookup"><span data-stu-id="f4500-144">If you're not comfortable with figuring out how to do the deployment steps on your own, it's better to follow the tutorial series from the [first tutorial](app-service-api-dotnet-get-started.md) than to start with this automated deployment process.</span></span>
> 
> 

1. <span data-ttu-id="f4500-145">Make sure that you have all of the prerequisites listed in the [first tutorial](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f4500-145">Make sure that you have all of the prerequisites listed in the [first tutorial](app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="f4500-146">In addition to the prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4500-146">In addition to the prerequisites listed, these authentication tutorials assume that you have worked with App Service web apps and API apps in Visual Studio and the Azure portal.</span></span>
2. <span data-ttu-id="f4500-147">Click the **Deploy to Azure** button in the [To Do List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) to deploy the API apps and the web app.</span><span class="sxs-lookup"><span data-stu-id="f4500-147">Click the **Deploy to Azure** button in the [To Do List sample repository readme file](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) to deploy the API apps and the web app.</span></span> <span data-ttu-id="f4500-148">Make a note of the Azure resource group that gets created, as you can use this later to look up web app and API app names.</span><span class="sxs-lookup"><span data-stu-id="f4500-148">Make a note of the Azure resource group that gets created, as you can use this later to look up web app and API app names.</span></span>
3. <span data-ttu-id="f4500-149">Download or clone the [To Do List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) to get the code that you'll work with locally in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f4500-149">Download or clone the [To Do List sample repository](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) to get the code that you'll work with locally in Visual Studio.</span></span>

## <a id="azureauth"></a> <span data-ttu-id="f4500-150">Set up authentication in App Service and Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4500-150">Set up authentication in App Service and Azure AD</span></span>
<span data-ttu-id="f4500-151">You now have the application running in Azure App Service without requiring that users be authenticated.</span><span class="sxs-lookup"><span data-stu-id="f4500-151">You now have the application running in Azure App Service without requiring that users be authenticated.</span></span> <span data-ttu-id="f4500-152">In this section you add authentication by doing the following tasks:</span><span class="sxs-lookup"><span data-stu-id="f4500-152">In this section you add authentication by doing the following tasks:</span></span>

* <span data-ttu-id="f4500-153">Configure App Service to require Azure Active Directory (Azure AD) authentication for calling the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-153">Configure App Service to require Azure Active Directory (Azure AD) authentication for calling the middle tier API app.</span></span>
* <span data-ttu-id="f4500-154">Create an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="f4500-154">Create an Azure AD application.</span></span>
* <span data-ttu-id="f4500-155">Configure the Azure AD application to send the bearer token after logon to the AngularJS front end.</span><span class="sxs-lookup"><span data-stu-id="f4500-155">Configure the Azure AD application to send the bearer token after logon to the AngularJS front end.</span></span> 

<span data-ttu-id="f4500-156">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span><span class="sxs-lookup"><span data-stu-id="f4500-156">If you run into problems while following the tutorial directions, see the [Troubleshooting](#troubleshooting) section at the end of the tutorial.</span></span> 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a><span data-ttu-id="f4500-157">Configure authentication for the middle tier API app</span><span class="sxs-lookup"><span data-stu-id="f4500-157">Configure authentication for the middle tier API app</span></span>
1. <span data-ttu-id="f4500-158">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListAPI project, find the **Features** section, and then click **Authentication / Authorization**.</span><span class="sxs-lookup"><span data-stu-id="f4500-158">In the [Azure portal](https://portal.azure.com/), navigate to the **Settings** blade of the API app that you created for the ToDoListAPI project, find the **Features** section, and then click **Authentication / Authorization**.</span></span>
   
    ![Azure portal Authentication/Authorization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/features.png)
2. <span data-ttu-id="f4500-160">In the **Authentication / Authorization** blade, click **On**.</span><span class="sxs-lookup"><span data-stu-id="f4500-160">In the **Authentication / Authorization** blade, click **On**.</span></span>
3. <span data-ttu-id="f4500-161">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4500-161">In the **Action to take when request is not authenticated** drop-down list, select **Log in with Azure Active Directory**.</span></span>
   
    <span data-ttu-id="f4500-162">This option ensures that no unauathenticated requests will reach the API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-162">This option ensures that no unauathenticated requests will reach the API app.</span></span> 
4. <span data-ttu-id="f4500-163">Under **Authentication Providers**, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4500-163">Under **Authentication Providers**, click **Azure Active Directory**.</span></span>
   
    ![Azure portal Authentication/Authorization blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. <span data-ttu-id="f4500-165">In the **Azure Active Directory Settings** blade, click **Express**</span><span class="sxs-lookup"><span data-stu-id="f4500-165">In the **Azure Active Directory Settings** blade, click **Express**</span></span>
   
    ![Azure portal Authentication/Authorization Express option](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    <span data-ttu-id="f4500-167">With the **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span><span class="sxs-lookup"><span data-stu-id="f4500-167">With the **Express** option, App Service can automatically create an Azure AD application in your Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant).</span></span> 
   
    <span data-ttu-id="f4500-168">You don't have to create a tenant, because every Azure account automatically has one.</span><span class="sxs-lookup"><span data-stu-id="f4500-168">You don't have to create a tenant, because every Azure account automatically has one.</span></span>
6. <span data-ttu-id="f4500-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice the value that is in the **Create App** text box; you'll look up this AAD application in the Azure classic portal later.</span><span class="sxs-lookup"><span data-stu-id="f4500-169">Under **Management mode**, click **Create New AD App** if it isn't already selected, and notice the value that is in the **Create App** text box; you'll look up this AAD application in the Azure classic portal later.</span></span>
   
    ![Azure portal Azure AD settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    <span data-ttu-id="f4500-171">Azure will automatically create an Azure AD application with the indicated name in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f4500-171">Azure will automatically create an Azure AD application with the indicated name in your Azure AD tenant.</span></span> <span data-ttu-id="f4500-172">By default, the Azure AD application is named the same as the API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-172">By default, the Azure AD application is named the same as the API app.</span></span> <span data-ttu-id="f4500-173">If you prefer, you can enter a different name.</span><span class="sxs-lookup"><span data-stu-id="f4500-173">If you prefer, you can enter a different name.</span></span>
7. <span data-ttu-id="f4500-174">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4500-174">Click **OK**.</span></span>
8. <span data-ttu-id="f4500-175">In the **Authentication / Authorization** blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4500-175">In the **Authentication / Authorization** blade, click **Save**.</span></span>
   
    ![Click Save](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/authsave.png)

<span data-ttu-id="f4500-177">Now only users in your Azure AD tenant can call the API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-177">Now only users in your Azure AD tenant can call the API app.</span></span>

### <a name="optional-test-the-api-app"></a><span data-ttu-id="f4500-178">Optional: Test the API app</span><span class="sxs-lookup"><span data-stu-id="f4500-178">Optional: Test the API app</span></span>
1. <span data-ttu-id="f4500-179">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span><span class="sxs-lookup"><span data-stu-id="f4500-179">In a browser go to the URL of the API app: in the **API app** blade in the Azure portal, click the link under **URL**.</span></span>  
   
    <span data-ttu-id="f4500-180">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-180">You are redirected to a login screen because unauthenticated requests are not allowed to reach the API app.</span></span>
   
    <span data-ttu-id="f4500-181">If your browser goes to the "successfully created" page, the browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the API app's URL.</span><span class="sxs-lookup"><span data-stu-id="f4500-181">If your browser goes to the "successfully created" page, the browser might already be logged on -- in that case, open an InPrivate or Incognito window and go to the API app's URL.</span></span>
2. <span data-ttu-id="f4500-182">Log on using credentials for a user in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f4500-182">Log on using credentials for a user in your Azure AD tenant.</span></span>
   
    <span data-ttu-id="f4500-183">When you're logged on, the "successfully created" page appears in the browser.</span><span class="sxs-lookup"><span data-stu-id="f4500-183">When you're logged on, the "successfully created" page appears in the browser.</span></span>
3. <span data-ttu-id="f4500-184">Close the browser.</span><span class="sxs-lookup"><span data-stu-id="f4500-184">Close the browser.</span></span>

### <a name="configure-the-azure-ad-application"></a><span data-ttu-id="f4500-185">Configure the Azure AD application</span><span class="sxs-lookup"><span data-stu-id="f4500-185">Configure the Azure AD application</span></span>
<span data-ttu-id="f4500-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span><span class="sxs-lookup"><span data-stu-id="f4500-186">When you configured Azure AD authentication, App Service created an Azure AD application for you.</span></span> <span data-ttu-id="f4500-187">By default the new Azure AD application was configured to provide the bearer token to the API app's URL.</span><span class="sxs-lookup"><span data-stu-id="f4500-187">By default the new Azure AD application was configured to provide the bearer token to the API app's URL.</span></span> <span data-ttu-id="f4500-188">In this section you configure the Azure AD application to provide the bearer token to the AngularJS front end instead of directly to the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-188">In this section you configure the Azure AD application to provide the bearer token to the AngularJS front end instead of directly to the middle tier API app.</span></span> <span data-ttu-id="f4500-189">The AngularJS front end will send the token to the API app when it calls the API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-189">The AngularJS front end will send the token to the API app when it calls the API app.</span></span>

> [!NOTE]
> <span data-ttu-id="f4500-190">To keep the process as simple as possible, this tutorial uses a single Azure AD application for both the front end and the middle tier API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-190">To keep the process as simple as possible, this tutorial uses a single Azure AD application for both the front end and the middle tier API app.</span></span> <span data-ttu-id="f4500-191">Another option is to use two Azure AD applications.</span><span class="sxs-lookup"><span data-stu-id="f4500-191">Another option is to use two Azure AD applications.</span></span> <span data-ttu-id="f4500-192">In that case you would have to give the front end's Azure AD application permission to call the middle tier's Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="f4500-192">In that case you would have to give the front end's Azure AD application permission to call the middle tier's Azure AD application.</span></span> <span data-ttu-id="f4500-193">This multi-application approach would give you more granular control over permissions to each tier.</span><span class="sxs-lookup"><span data-stu-id="f4500-193">This multi-application approach would give you more granular control over permissions to each tier.</span></span>
> 
> 

1. <span data-ttu-id="f4500-194">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4500-194">In the [Azure classic portal](https://manage.windowsazure.com/), go to **Azure Active Directory**.</span></span>
   
   <span data-ttu-id="f4500-195">You have to use the classic portal because certain Azure Active Directory settings that you need access to are not yet available in the current Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f4500-195">You have to use the classic portal because certain Azure Active Directory settings that you need access to are not yet available in the current Azure portal.</span></span>
2. <span data-ttu-id="f4500-196">On the **Directory** tab, click your AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="f4500-196">On the **Directory** tab, click your AAD tenant.</span></span>
   
   ![Azure AD in classic portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. <span data-ttu-id="f4500-198">Click **Applications > Applications my company owns**, and then click the check mark.</span><span class="sxs-lookup"><span data-stu-id="f4500-198">Click **Applications > Applications my company owns**, and then click the check mark.</span></span>
   
   <span data-ttu-id="f4500-199">You might also have to refresh the page to see the new application.</span><span class="sxs-lookup"><span data-stu-id="f4500-199">You might also have to refresh the page to see the new application.</span></span>
4. <span data-ttu-id="f4500-200">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for your API app.</span><span class="sxs-lookup"><span data-stu-id="f4500-200">In the list of applications, click the name of the one that Azure created for you when you enabled authentication for your API app.</span></span>
   
   ![Azure AD Applications tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. <span data-ttu-id="f4500-202">Click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="f4500-202">Click **Configure**.</span></span>
   
   ![Azure AD Configure tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/configure.png)
6. <span data-ttu-id="f4500-204">Set **Sign-on URL** to the URL for your AngularJS web app, no trailing slash.</span><span class="sxs-lookup"><span data-stu-id="f4500-204">Set **Sign-on URL** to the URL for your AngularJS web app, no trailing slash.</span></span>
   
   <span data-ttu-id="f4500-205">For example: https://todolistangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f4500-205">For example: https://todolistangular.azurewebsites.net</span></span>
   
   ![Sign-on URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. <span data-ttu-id="f4500-207">Set **Reply URL** to the URL for your web app, no trailing slash.</span><span class="sxs-lookup"><span data-stu-id="f4500-207">Set **Reply URL** to the URL for your web app, no trailing slash.</span></span>
   
   <span data-ttu-id="f4500-208">For example: https://todolistsangular.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="f4500-208">For example: https://todolistsangular.azurewebsites.net</span></span>
8. <span data-ttu-id="f4500-209">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f4500-209">Click **Save**.</span></span>
   
   ![Reply URL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. <span data-ttu-id="f4500-211">At the bottom of the page, click **Manage manifest > Download manifest**.</span><span class="sxs-lookup"><span data-stu-id="f4500-211">At the bottom of the page, click **Manage manifest > Download manifest**.</span></span>
   
   ![Download manifest](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. <span data-ttu-id="f4500-213">Download the file to a location where you can edit it.</span><span class="sxs-lookup"><span data-stu-id="f4500-213">Download the file to a location where you can edit it.</span></span>
11. <span data-ttu-id="f4500-214">In the downloaded manifest file, search for the  `oauth2AllowImplicitFlow` property.</span><span class="sxs-lookup"><span data-stu-id="f4500-214">In the downloaded manifest file, search for the  `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="f4500-215">Change the value of this property from `false` to `true`, and then save the file.</span><span class="sxs-lookup"><span data-stu-id="f4500-215">Change the value of this property from `false` to `true`, and then save the file.</span></span>
    
    <span data-ttu-id="f4500-216">This setting is required for access from a JavaScript single-page application.</span><span class="sxs-lookup"><span data-stu-id="f4500-216">This setting is required for access from a JavaScript single-page application.</span></span> <span data-ttu-id="f4500-217">It enables the Oauth 2.0 bearer token to be returned in the URL fragment.</span><span class="sxs-lookup"><span data-stu-id="f4500-217">It enables the Oauth 2.0 bearer token to be returned in the URL fragment.</span></span>
12. <span data-ttu-id="f4500-218">Click **Manage manifest > Upload manifest**, and upload the file that you updated in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="f4500-218">Click **Manage manifest > Upload manifest**, and upload the file that you updated in the preceding step.</span></span>
    
    ![Upload manifest](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. <span data-ttu-id="f4500-220">Copy the **Client ID** value and save it somewhere you can get it from later.</span><span class="sxs-lookup"><span data-stu-id="f4500-220">Copy the **Client ID** value and save it somewhere you can get it from later.</span></span>

## <a name="configure-the-todolistangular-project-to-use-authentication"></a><span data-ttu-id="f4500-221">Configure the ToDoListAngular project to use authentication</span><span class="sxs-lookup"><span data-stu-id="f4500-221">Configure the ToDoListAngular project to use authentication</span></span>
<span data-ttu-id="f4500-222">In this section you change the AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS to acquire a bearer token for the logged-on user from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4500-222">In this section you change the AngularJS front end so that it uses Active Directory Authentication Library (ADAL) for JS to acquire a bearer token for the logged-on user from Azure AD.</span></span> <span data-ttu-id="f4500-223">The code will include the token in HTTP requests sent to the middle tier, as shown in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="f4500-223">The code will include the token in HTTP requests sent to the middle tier, as shown in the following diagram.</span></span> 

![User authentication diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

<span data-ttu-id="f4500-225">Make the following changes to files in the ToDoListAngular project.</span><span class="sxs-lookup"><span data-stu-id="f4500-225">Make the following changes to files in the ToDoListAngular project.</span></span>

1. <span data-ttu-id="f4500-226">Open the *index.cshtml* file.</span><span class="sxs-lookup"><span data-stu-id="f4500-226">Open the *index.cshtml* file.</span></span>
2. <span data-ttu-id="f4500-227">Uncomment the lines that reference the Active Directory Authentication Library (ADAL) for JS scripts.</span><span class="sxs-lookup"><span data-stu-id="f4500-227">Uncomment the lines that reference the Active Directory Authentication Library (ADAL) for JS scripts.</span></span>
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. <span data-ttu-id="f4500-228">Open the *app/scripts/app.js* file.</span><span class="sxs-lookup"><span data-stu-id="f4500-228">Open the *app/scripts/app.js* file.</span></span>
4. <span data-ttu-id="f4500-229">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span><span class="sxs-lookup"><span data-stu-id="f4500-229">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
   
    <span data-ttu-id="f4500-230">This change references the ADAL JS authentication provider and provides configuration values to it.</span><span class="sxs-lookup"><span data-stu-id="f4500-230">This change references the ADAL JS authentication provider and provides configuration values to it.</span></span> <span data-ttu-id="f4500-231">In the following steps you set the configuration values for your API app and Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="f4500-231">In the following steps you set the configuration values for your API app and Azure AD application.</span></span>
5. <span data-ttu-id="f4500-232">In the code that sets the `endpoints` variable, set the API URL to the URL of the API app that you created for the ToDoListAPI project, and set the Azure AD application ID to the client ID that you copied from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f4500-232">In the code that sets the `endpoints` variable, set the API URL to the URL of the API app that you created for the ToDoListAPI project, and set the Azure AD application ID to the client ID that you copied from the Azure classic portal.</span></span>
   
    <span data-ttu-id="f4500-233">The code is now similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f4500-233">The code is now similar to the following example.</span></span>
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. <span data-ttu-id="f4500-234">In the call to `adalProvider.init`, set `tenant` to your tenant name and `clientId` to same value you used in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f4500-234">In the call to `adalProvider.init`, set `tenant` to your tenant name and `clientId` to same value you used in the previous step.</span></span>
   
    <span data-ttu-id="f4500-235">The code is now similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="f4500-235">The code is now similar to the following example.</span></span>
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    <span data-ttu-id="f4500-236">These changes to `app.js` specify that the calling code and the called API are in the same Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="f4500-236">These changes to `app.js` specify that the calling code and the called API are in the same Azure AD application.</span></span>
7. <span data-ttu-id="f4500-237">Open the *app/scripts/homeCtrl.js* file.</span><span class="sxs-lookup"><span data-stu-id="f4500-237">Open the *app/scripts/homeCtrl.js* file.</span></span>
8. <span data-ttu-id="f4500-238">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span><span class="sxs-lookup"><span data-stu-id="f4500-238">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>
9. <span data-ttu-id="f4500-239">Open the *app/scripts/indexCtrl.js* file.</span><span class="sxs-lookup"><span data-stu-id="f4500-239">Open the *app/scripts/indexCtrl.js* file.</span></span>
10. <span data-ttu-id="f4500-240">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span><span class="sxs-lookup"><span data-stu-id="f4500-240">Comment out the block of code marked for "without authentication" and uncomment the block of code marked for "with authentication".</span></span>

### <a name="deploy-the-todolistangular-project-to-azure"></a><span data-ttu-id="f4500-241">Deploy the ToDoListAngular project to Azure</span><span class="sxs-lookup"><span data-stu-id="f4500-241">Deploy the ToDoListAngular project to Azure</span></span>
1. <span data-ttu-id="f4500-242">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4500-242">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f4500-243">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4500-243">Click **Publish**.</span></span>
   
    <span data-ttu-id="f4500-244">Visual Studio deploys the project and opens a browser to the web app's base URL.</span><span class="sxs-lookup"><span data-stu-id="f4500-244">Visual Studio deploys the project and opens a browser to the web app's base URL.</span></span> <span data-ttu-id="f4500-245">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span><span class="sxs-lookup"><span data-stu-id="f4500-245">This will show a 403 error page, which is normal for an attempt to go to a Web API base URL from a browser.</span></span>
   
    <span data-ttu-id="f4500-246">You still have to make a change to the middle tier API app before you can test the application.</span><span class="sxs-lookup"><span data-stu-id="f4500-246">You still have to make a change to the middle tier API app before you can test the application.</span></span>
3. <span data-ttu-id="f4500-247">Close the browser.</span><span class="sxs-lookup"><span data-stu-id="f4500-247">Close the browser.</span></span>

## <a name="configure-the-todolistapi-project-to-use-authentication"></a><span data-ttu-id="f4500-248">Configure the ToDoListAPI project to use authentication</span><span class="sxs-lookup"><span data-stu-id="f4500-248">Configure the ToDoListAPI project to use authentication</span></span>
<span data-ttu-id="f4500-249">Currently the ToDoListAPI project sends "\*" as the `owner` value to ToDoListDataAPI.</span><span class="sxs-lookup"><span data-stu-id="f4500-249">Currently the ToDoListAPI project sends "\*" as the `owner` value to ToDoListDataAPI.</span></span> <span data-ttu-id="f4500-250">In this section you change the code to send the ID of the logged-on user.</span><span class="sxs-lookup"><span data-stu-id="f4500-250">In this section you change the code to send the ID of the logged-on user.</span></span>

<span data-ttu-id="f4500-251">Make the following changes in the ToDoListAPI project.</span><span class="sxs-lookup"><span data-stu-id="f4500-251">Make the following changes in the ToDoListAPI project.</span></span>

1. <span data-ttu-id="f4500-252">Open the *Controllers/ToDoListController.cs* file, and uncomment the line in each action method that sets `owner` to the Azure AD `NameIdentifier` claim value.</span><span class="sxs-lookup"><span data-stu-id="f4500-252">Open the *Controllers/ToDoListController.cs* file, and uncomment the line in each action method that sets `owner` to the Azure AD `NameIdentifier` claim value.</span></span> <span data-ttu-id="f4500-253">For example:</span><span class="sxs-lookup"><span data-stu-id="f4500-253">For example:</span></span>
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    <span data-ttu-id="f4500-254">**Important**: Don't uncomment code in the `ToDoListDataAPI` method; you'll do that later for the service principal authentication tutorial.</span><span class="sxs-lookup"><span data-stu-id="f4500-254">**Important**: Don't uncomment code in the `ToDoListDataAPI` method; you'll do that later for the service principal authentication tutorial.</span></span>

### <a name="deploy-the-todolistapi-project-to-azure"></a><span data-ttu-id="f4500-255">Deploy the ToDoListAPI project to Azure</span><span class="sxs-lookup"><span data-stu-id="f4500-255">Deploy the ToDoListAPI project to Azure</span></span>
1. <span data-ttu-id="f4500-256">In **Solution Explorer**, right-click the ToDoListAPI project, and then click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4500-256">In **Solution Explorer**, right-click the ToDoListAPI project, and then click **Publish**.</span></span>
2. <span data-ttu-id="f4500-257">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4500-257">Click **Publish**.</span></span>
   
    <span data-ttu-id="f4500-258">Visual Studio deploys the project and opens a browser to the API app's base URL.</span><span class="sxs-lookup"><span data-stu-id="f4500-258">Visual Studio deploys the project and opens a browser to the API app's base URL.</span></span>
3. <span data-ttu-id="f4500-259">Close the browser.</span><span class="sxs-lookup"><span data-stu-id="f4500-259">Close the browser.</span></span>

### <a name="test-the-application"></a><span data-ttu-id="f4500-260">Test the application</span><span class="sxs-lookup"><span data-stu-id="f4500-260">Test the application</span></span>
1. <span data-ttu-id="f4500-261">Go to the URL of the web app, **using HTTPS, not HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f4500-261">Go to the URL of the web app, **using HTTPS, not HTTP**.</span></span>
2. <span data-ttu-id="f4500-262">Click the **To Do List** tab.</span><span class="sxs-lookup"><span data-stu-id="f4500-262">Click the **To Do List** tab.</span></span>
   
    <span data-ttu-id="f4500-263">You are prompted to log in.</span><span class="sxs-lookup"><span data-stu-id="f4500-263">You are prompted to log in.</span></span>
3. <span data-ttu-id="f4500-264">Log in with the credentials of a user in your AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="f4500-264">Log in with the credentials of a user in your AAD tenant.</span></span>
4. <span data-ttu-id="f4500-265">The **To Do List** page appears.</span><span class="sxs-lookup"><span data-stu-id="f4500-265">The **To Do List** page appears.</span></span>
   
   ![To Do List page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   <span data-ttu-id="f4500-267">No to-do items are displayed because until now they have all been for owner "\*".</span><span class="sxs-lookup"><span data-stu-id="f4500-267">No to-do items are displayed because until now they have all been for owner "\*".</span></span> <span data-ttu-id="f4500-268">Now the middle tier is requesting items for the logged-on user, and none have been created yet.</span><span class="sxs-lookup"><span data-stu-id="f4500-268">Now the middle tier is requesting items for the logged-on user, and none have been created yet.</span></span>
5. <span data-ttu-id="f4500-269">Add new to-do items to verify that the application is working.</span><span class="sxs-lookup"><span data-stu-id="f4500-269">Add new to-do items to verify that the application is working.</span></span>
6. <span data-ttu-id="f4500-270">In another browser window, go to the Swagger UI URL for the ToDoListDataAPI API app and click **ToDoList > Get**.</span><span class="sxs-lookup"><span data-stu-id="f4500-270">In another browser window, go to the Swagger UI URL for the ToDoListDataAPI API app and click **ToDoList > Get**.</span></span> <span data-ttu-id="f4500-271">Enter an asterisk for the `owner` parameter, and then click **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="f4500-271">Enter an asterisk for the `owner` parameter, and then click **Try it out**.</span></span>
   
   <span data-ttu-id="f4500-272">The response shows that the new to-do items have the actual Azure AD user ID in the Owner property.</span><span class="sxs-lookup"><span data-stu-id="f4500-272">The response shows that the new to-do items have the actual Azure AD user ID in the Owner property.</span></span>
   
   ![Owner ID in JSON response](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-api/media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a><span data-ttu-id="f4500-274">Building the projects from scratch</span><span class="sxs-lookup"><span data-stu-id="f4500-274">Building the projects from scratch</span></span>
<span data-ttu-id="f4500-275">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span><span class="sxs-lookup"><span data-stu-id="f4500-275">The two Web API projects were created by using the **Azure API App** project template and replacing the default Values controller with a ToDoList controller.</span></span> 

<span data-ttu-id="f4500-276">For information about how to  create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span><span class="sxs-lookup"><span data-stu-id="f4500-276">For information about how to  create an AngularJS single-page application with a Web API 2 back end, see  [Hands On Lab: Build a Single Page Application (SPA) with ASP.NET Web API and Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs).</span></span> <span data-ttu-id="f4500-277">For information about how to add Azure AD authentication code, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="f4500-277">For information about how to add Azure AD authentication code, see the following resources:</span></span>

* <span data-ttu-id="f4500-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span><span class="sxs-lookup"><span data-stu-id="f4500-278">[Securing AngularJS Single Page Apps with Azure AD](../active-directory/active-directory-devquickstarts-angular.md).</span></span>
* [<span data-ttu-id="f4500-279">Introducing ADAL JS v1</span><span class="sxs-lookup"><span data-stu-id="f4500-279">Introducing ADAL JS v1</span></span>](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a><span data-ttu-id="f4500-280">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="f4500-280">Troubleshooting</span></span>
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* <span data-ttu-id="f4500-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span><span class="sxs-lookup"><span data-stu-id="f4500-281">Make sure that you don't confuse ToDoListAPI (middle tier) and ToDoListDataAPI (data tier).</span></span> <span data-ttu-id="f4500-282">For example, verify that you added authentication to the middle tier API app, not the data tier.</span><span class="sxs-lookup"><span data-stu-id="f4500-282">For example, verify that you added authentication to the middle tier API app, not the data tier.</span></span> 
* <span data-ttu-id="f4500-283">Make sure that the AngularJS source code references the middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and the correct Azure AD client ID.</span><span class="sxs-lookup"><span data-stu-id="f4500-283">Make sure that the AngularJS source code references the middle tier API app URL (ToDoListAPI, not ToDoListDataAPI)and the correct Azure AD client ID.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f4500-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4500-284">Next steps</span></span>
<span data-ttu-id="f4500-285">In this tutorial you learned how to use App Service authentication for an API app and how to call the API app by using the ADAL JS library.</span><span class="sxs-lookup"><span data-stu-id="f4500-285">In this tutorial you learned how to use App Service authentication for an API app and how to call the API app by using the ADAL JS library.</span></span> <span data-ttu-id="f4500-286">In the next tutorial you'll learn how to [secure access to your API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="f4500-286">In the next tutorial you'll learn how to [secure access to your API app for service-to-service scenarios](app-service-api-dotnet-service-principal-auth.md).</span></span>


















