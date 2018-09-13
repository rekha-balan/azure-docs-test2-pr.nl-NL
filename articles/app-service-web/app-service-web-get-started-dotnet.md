---
title: Create your first ASP.NET web app in Azure in five minutes | Microsoft Docs
description: Learn how easy it is to run web apps in App Service by deploying a simple ASP.NET application.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: wpickett
editor: ''
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: cephalin
ms.openlocfilehash: 8705975a4278987f7fb5902e59ab13848d44f972
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549862"
---
# <a name="create-your-first-aspnet-web-app-in-azure-in-five-minutes"></a><span data-ttu-id="7c5da-103">Create your first ASP.NET web app in Azure in five minutes</span><span class="sxs-lookup"><span data-stu-id="7c5da-103">Create your first ASP.NET web app in Azure in five minutes</span></span>

[!INCLUDE [app-service-web-selector-get-started](../../includes/app-service-web-selector-get-started.md)] 

<span data-ttu-id="7c5da-104">This Quickstart helps you deploy your first ASP.NET web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="7c5da-104">This Quickstart helps you deploy your first ASP.NET web app to [Azure App Service](../app-service/app-service-value-prop-what-is.md) in just a few minutes.</span></span> <span data-ttu-id="7c5da-105">When you're finished, you'll have a simple web app up and running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="7c5da-105">When you're finished, you'll have a simple web app up and running in the cloud.</span></span>

![ASP.NET web app in Azure App Service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="before-you-begin"></a><span data-ttu-id="7c5da-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="7c5da-107">Before you begin</span></span>

<span data-ttu-id="7c5da-108">This tutorial demonstrates how to use Visual Studio 2017 to build and deploy an ASP.NET web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5da-108">This tutorial demonstrates how to use Visual Studio 2017 to build and deploy an ASP.NET web app to Azure.</span></span> <span data-ttu-id="7c5da-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7c5da-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="7c5da-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="7c5da-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="7c5da-111">Create an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="7c5da-111">Create an ASP.NET web app</span></span>

<span data-ttu-id="7c5da-112">In Visual Studio, create a new project with `Ctrl`+`Shift`+`N`.</span><span class="sxs-lookup"><span data-stu-id="7c5da-112">In Visual Studio, create a new project with `Ctrl`+`Shift`+`N`.</span></span>

<span data-ttu-id="7c5da-113">In the **New Project** dialog, click **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-113">In the **New Project** dialog, click **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="7c5da-114">Name the application **myFirstAzureWebApp**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-114">Name the application **myFirstAzureWebApp**, and then click **OK**.</span></span>
   
![New Project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="7c5da-116">You can deploy any type of ASP.NET web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5da-116">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="7c5da-117">For this tutorial, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-117">For this tutorial, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="7c5da-118">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-118">Click **OK**.</span></span>

![New ASP.NET Project dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/select-mvc-template.png)

## <a name="publish-to-azure"></a><span data-ttu-id="7c5da-120">Publish to Azure</span><span class="sxs-lookup"><span data-stu-id="7c5da-120">Publish to Azure</span></span>

<span data-ttu-id="7c5da-121">In the **Solution Explorer**, right-click your **myFirstAzureWebApp** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-121">In the **Solution Explorer**, right-click your **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publish from Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="7c5da-123">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-123">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publish from project overview page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="7c5da-125">This opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5da-125">This opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="7c5da-126">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="7c5da-126">Sign in to Azure</span></span>

<span data-ttu-id="7c5da-127">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7c5da-127">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="7c5da-128">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7c5da-128">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="7c5da-129">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span><span class="sxs-lookup"><span data-stu-id="7c5da-129">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Sign in to Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/sign-in-azure.png)

<span data-ttu-id="7c5da-131">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span><span class="sxs-lookup"><span data-stu-id="7c5da-131">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="7c5da-132">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="7c5da-132">Create a resource group</span></span>

<span data-ttu-id="7c5da-133">First, you need a _resource group_.</span><span class="sxs-lookup"><span data-stu-id="7c5da-133">First, you need a _resource group_.</span></span> 

> [!NOTE] 
> <span data-ttu-id="7c5da-134">A resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="7c5da-134">A resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span>
>
>

<span data-ttu-id="7c5da-135">Next to **Resource Group**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-135">Next to **Resource Group**, click **New**.</span></span>

<span data-ttu-id="7c5da-136">Name your resource group **myResourceGroup** and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-136">Name your resource group **myResourceGroup** and click **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="7c5da-137">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="7c5da-137">Create an App Service plan</span></span>

<span data-ttu-id="7c5da-138">Your Azure web app also needs an _App Service plan_.</span><span class="sxs-lookup"><span data-stu-id="7c5da-138">Your Azure web app also needs an _App Service plan_.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c5da-139">An App Service plan represents the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="7c5da-139">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="7c5da-140">All apps assigned to an App Service plan share the resources defined by it, which enables you to save cost when hosting multiple apps.</span><span class="sxs-lookup"><span data-stu-id="7c5da-140">All apps assigned to an App Service plan share the resources defined by it, which enables you to save cost when hosting multiple apps.</span></span> 
>
> <span data-ttu-id="7c5da-141">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="7c5da-141">App Service plans define:</span></span>
>
> - <span data-ttu-id="7c5da-142">Region (North Europe, East US, Southeast Asia)</span><span class="sxs-lookup"><span data-stu-id="7c5da-142">Region (North Europe, East US, Southeast Asia)</span></span>
> - <span data-ttu-id="7c5da-143">Instance Size (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="7c5da-143">Instance Size (Small, Medium, Large)</span></span>
> - <span data-ttu-id="7c5da-144">Scale Count (one, two or three instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="7c5da-144">Scale Count (one, two or three instances, etc.)</span></span> 
> - <span data-ttu-id="7c5da-145">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="7c5da-145">SKU (Free, Shared, Basic, Standard, Premium)</span></span>
>
>

<span data-ttu-id="7c5da-146">Next to **App Service Plan**, click **New**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-146">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="7c5da-147">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span><span class="sxs-lookup"><span data-stu-id="7c5da-147">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

- <span data-ttu-id="7c5da-148">**App Service Plan**: Type **myAppServicePlan**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-148">**App Service Plan**: Type **myAppServicePlan**.</span></span> 
- <span data-ttu-id="7c5da-149">**Location**: Choose **West Europe**, or any other region you like.</span><span class="sxs-lookup"><span data-stu-id="7c5da-149">**Location**: Choose **West Europe**, or any other region you like.</span></span>
- <span data-ttu-id="7c5da-150">**Size**: Choose **Free**, or any other [pricing tier](https://azure.microsoft.com/pricing/details/app-service/) you like.</span><span class="sxs-lookup"><span data-stu-id="7c5da-150">**Size**: Choose **Free**, or any other [pricing tier](https://azure.microsoft.com/pricing/details/app-service/) you like.</span></span>

<span data-ttu-id="7c5da-151">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-151">Click **OK**.</span></span>

![Create new App Service plan](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="7c5da-153">Create and publish the web app</span><span class="sxs-lookup"><span data-stu-id="7c5da-153">Create and publish the web app</span></span>

<span data-ttu-id="7c5da-154">The only thing left to do now is to name your web app.</span><span class="sxs-lookup"><span data-stu-id="7c5da-154">The only thing left to do now is to name your web app.</span></span> <span data-ttu-id="7c5da-155">In **Web App Name**, type a unique app name.</span><span class="sxs-lookup"><span data-stu-id="7c5da-155">In **Web App Name**, type a unique app name.</span></span> <span data-ttu-id="7c5da-156">This name will be used as part of the default DNS name for your app (`<app_name>.azurewebsites.net`), so it needs to be unique across all apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5da-156">This name will be used as part of the default DNS name for your app (`<app_name>.azurewebsites.net`), so it needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="7c5da-157">You can later map a custom domain name to your app before you expose it to your users.</span><span class="sxs-lookup"><span data-stu-id="7c5da-157">You can later map a custom domain name to your app before you expose it to your users.</span></span>

<span data-ttu-id="7c5da-158">You can also accept the automatically generated name, which is already unique.</span><span class="sxs-lookup"><span data-stu-id="7c5da-158">You can also accept the automatically generated name, which is already unique.</span></span>

<span data-ttu-id="7c5da-159">Click **Create** to start creating the Azure resources.</span><span class="sxs-lookup"><span data-stu-id="7c5da-159">Click **Create** to start creating the Azure resources.</span></span>

![Configure web app name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="7c5da-161">Once the wizard finishes creating the Azure resources, it automatically publishes your ASP.NET web app to Azure for the first time, and then launches the published Azure web app in your default browser.</span><span class="sxs-lookup"><span data-stu-id="7c5da-161">Once the wizard finishes creating the Azure resources, it automatically publishes your ASP.NET web app to Azure for the first time, and then launches the published Azure web app in your default browser.</span></span>

![Published ASP.NET web app in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="7c5da-163">The URL uses the web app name that you specified earlier, with the format `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="7c5da-163">The URL uses the web app name that you specified earlier, with the format `http://<app_name>.azurewebsites.net`.</span></span> 

<span data-ttu-id="7c5da-164">Congratulations, your first ASP.NET web app is running live in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="7c5da-164">Congratulations, your first ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="7c5da-165">Update the app and redeploy</span><span class="sxs-lookup"><span data-stu-id="7c5da-165">Update the app and redeploy</span></span>

<span data-ttu-id="7c5da-166">It's very easy to redeploy an update to Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5da-166">It's very easy to redeploy an update to Azure.</span></span> <span data-ttu-id="7c5da-167">Let's make an update to the homepage.</span><span class="sxs-lookup"><span data-stu-id="7c5da-167">Let's make an update to the homepage.</span></span>

<span data-ttu-id="7c5da-168">From the **Solution Explorer**, open **Views\Home\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-168">From the **Solution Explorer**, open **Views\Home\Index.cshtml**.</span></span>

<span data-ttu-id="7c5da-169">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire tag with the following code:</span><span class="sxs-lookup"><span data-stu-id="7c5da-169">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire tag with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="7c5da-170">To redeploy to Azure, right-click youre **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-170">To redeploy to Azure, right-click youre **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="7c5da-171">In the publish page, click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-171">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="7c5da-172">When Visual Studio is finished, it launches the updated Azure web app in your browser.</span><span class="sxs-lookup"><span data-stu-id="7c5da-172">When Visual Studio is finished, it launches the updated Azure web app in your browser.</span></span>

![Updated ASP.NET web app in Azure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="7c5da-174">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="7c5da-174">Manage your new Azure web app</span></span>

<span data-ttu-id="7c5da-175">Go to the Azure portal to take a look at the web app you just created.</span><span class="sxs-lookup"><span data-stu-id="7c5da-175">Go to the Azure portal to take a look at the web app you just created.</span></span> 

<span data-ttu-id="7c5da-176">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c5da-176">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="7c5da-177">From the left menu, click **App Services**, then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="7c5da-177">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="7c5da-179">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span><span class="sxs-lookup"><span data-stu-id="7c5da-179">You have landed in your web app's _blade_ (a portal page that opens horizontally).</span></span> 

<span data-ttu-id="7c5da-180">By default, your web app's blade shows the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="7c5da-180">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="7c5da-181">This page gives you a view of how your app is doing.</span><span class="sxs-lookup"><span data-stu-id="7c5da-181">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="7c5da-182">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="7c5da-182">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="7c5da-183">The tabs on the left side of the blade shows the different configuration pages you can open.</span><span class="sxs-lookup"><span data-stu-id="7c5da-183">The tabs on the left side of the blade shows the different configuration pages you can open.</span></span> 

![App Service blade in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="7c5da-185">These tabs in the blade show the many great features you can add to your web app.</span><span class="sxs-lookup"><span data-stu-id="7c5da-185">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="7c5da-186">The following list gives you just a few of the possibilities:</span><span class="sxs-lookup"><span data-stu-id="7c5da-186">The following list gives you just a few of the possibilities:</span></span>

- <span data-ttu-id="7c5da-187">Map a custom DNS name</span><span class="sxs-lookup"><span data-stu-id="7c5da-187">Map a custom DNS name</span></span>
- <span data-ttu-id="7c5da-188">Bind a custom SSL certificate</span><span class="sxs-lookup"><span data-stu-id="7c5da-188">Bind a custom SSL certificate</span></span>
- <span data-ttu-id="7c5da-189">Configure continuous deployment</span><span class="sxs-lookup"><span data-stu-id="7c5da-189">Configure continuous deployment</span></span>
- <span data-ttu-id="7c5da-190">Scale up and out</span><span class="sxs-lookup"><span data-stu-id="7c5da-190">Scale up and out</span></span>
- <span data-ttu-id="7c5da-191">Add user authentication</span><span class="sxs-lookup"><span data-stu-id="7c5da-191">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7c5da-192">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="7c5da-192">Clean up resources</span></span>

<span data-ttu-id="7c5da-193">To delete your first Azure web app, you can click **Delete** in the **Overview** page.</span><span class="sxs-lookup"><span data-stu-id="7c5da-193">To delete your first Azure web app, you can click **Delete** in the **Overview** page.</span></span> <span data-ttu-id="7c5da-194">However, there's a better way to delete everything that you created in this quick start.</span><span class="sxs-lookup"><span data-stu-id="7c5da-194">However, there's a better way to delete everything that you created in this quick start.</span></span> <span data-ttu-id="7c5da-195">From your web app's **Overview** page, click the resource group to open its blade.</span><span class="sxs-lookup"><span data-stu-id="7c5da-195">From your web app's **Overview** page, click the resource group to open its blade.</span></span> 

![Access resource group from App Service blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/access-resource-group.png)

<span data-ttu-id="7c5da-197">In the resource group blade, you can see both the App Service plan and the App Service app that Visual Studio created for you.</span><span class="sxs-lookup"><span data-stu-id="7c5da-197">In the resource group blade, you can see both the App Service plan and the App Service app that Visual Studio created for you.</span></span> 

<span data-ttu-id="7c5da-198">At the top of the blade, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-198">At the top of the blade, click **Delete**.</span></span> 

<!--![Delete resource group in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/app-service-web-get-started-dotnet/delete-resource-group.png)-->

<span data-ttu-id="7c5da-199">In the confirmation blade, confirm by typing the resource group name **myResourceGroup** into the text box and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="7c5da-199">In the confirmation blade, confirm by typing the resource group name **myResourceGroup** into the text box and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c5da-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c5da-200">Next steps</span></span>

<span data-ttu-id="7c5da-201">Explore pre-created [Web apps PowerShell scripts](app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c5da-201">Explore pre-created [Web apps PowerShell scripts](app-service-powershell-samples.md).</span></span>














