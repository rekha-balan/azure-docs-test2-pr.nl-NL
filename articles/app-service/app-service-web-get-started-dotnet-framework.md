---
title: Create a C# ASP.NET Framework web app in Azure | Microsoft Docs
description: Learn how to run web apps in Azure App Service by deploying the default C# ASP.NET web app.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: 04a1becf-7756-4d4e-92d8-d9471c263d23
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: cephalin
ms.custom: mvc, devcenter
ms.openlocfilehash: cce14d91509fe051beef87acdaeac9a92d998ef6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871001"
---
# <a name="create-an-aspnet-framework-web-app-in-azure"></a><span data-ttu-id="c4645-103">Create an ASP.NET Framework web app in Azure</span><span class="sxs-lookup"><span data-stu-id="c4645-103">Create an ASP.NET Framework web app in Azure</span></span>

<span data-ttu-id="c4645-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="c4645-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="c4645-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="c4645-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="c4645-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span><span class="sxs-lookup"><span data-stu-id="c4645-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

![](./media/app-service-web-get-started-dotnet-framework/published-azure-web-app.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="c4645-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4645-107">Prerequisites</span></span>

<span data-ttu-id="c4645-108">To complete this tutorial, install <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="c4645-108">To complete this tutorial, install <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> with the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="c4645-109">If you've installed Visual Studio 2017 already:</span><span class="sxs-lookup"><span data-stu-id="c4645-109">If you've installed Visual Studio 2017 already:</span></span>

- <span data-ttu-id="c4645-110">Install the latest updates in Visual Studio by clicking **Help** > **Check for Updates**.</span><span class="sxs-lookup"><span data-stu-id="c4645-110">Install the latest updates in Visual Studio by clicking **Help** > **Check for Updates**.</span></span>
- <span data-ttu-id="c4645-111">Add the workload by clicking **Tools** > **Get Tools and Features**.</span><span class="sxs-lookup"><span data-stu-id="c4645-111">Add the workload by clicking **Tools** > **Get Tools and Features**.</span></span>

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="c4645-112">Create an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="c4645-112">Create an ASP.NET web app</span></span>

<span data-ttu-id="c4645-113">In Visual Studio, create a project by selecting **File > New > Project**.</span><span class="sxs-lookup"><span data-stu-id="c4645-113">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="c4645-114">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c4645-114">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="c4645-115">Name the application _myFirstAzureWebApp_, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4645-115">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![New Project dialog box](./media/app-service-web-get-started-dotnet-framework/new-project.png)

<span data-ttu-id="c4645-117">You can deploy any type of ASP.NET web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="c4645-117">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="c4645-118">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span><span class="sxs-lookup"><span data-stu-id="c4645-118">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="c4645-119">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4645-119">Select **OK**.</span></span>

![New ASP.NET Project dialog box](./media/app-service-web-get-started-dotnet-framework/select-mvc-template.png)

<span data-ttu-id="c4645-121">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="c4645-121">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Run app locally](./media/app-service-web-get-started-dotnet-framework/local-web-app.png)

## <a name="launch-the-publish-wizard"></a><span data-ttu-id="c4645-123">Launch the publish wizard</span><span class="sxs-lookup"><span data-stu-id="c4645-123">Launch the publish wizard</span></span>

<span data-ttu-id="c4645-124">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c4645-124">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publish from Solution Explorer](./media/app-service-web-get-started-dotnet-framework/solution-explorer-publish.png)

<span data-ttu-id="c4645-126">The publish wizard is automatically launched.</span><span class="sxs-lookup"><span data-stu-id="c4645-126">The publish wizard is automatically launched.</span></span> <span data-ttu-id="c4645-127">Select **App Service** > **Publish** to open the **Create App Service** dialog.</span><span class="sxs-lookup"><span data-stu-id="c4645-127">Select **App Service** > **Publish** to open the **Create App Service** dialog.</span></span>

![Publish from project overview page](./media/app-service-web-get-started-dotnet-framework/publish-to-app-service.png)

## <a name="sign-in-to-azure"></a><span data-ttu-id="c4645-129">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="c4645-129">Sign in to Azure</span></span>

<span data-ttu-id="c4645-130">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c4645-130">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="c4645-131">If you're already signed in, select the account containing the desired subscription from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="c4645-131">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="c4645-132">If you're already signed in, don't select **Create** yet.</span><span class="sxs-lookup"><span data-stu-id="c4645-132">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Sign in to Azure](./media/app-service-web-get-started-dotnet-framework/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="c4645-134">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="c4645-134">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="c4645-135">Next to **Resource Group**, select **New**.</span><span class="sxs-lookup"><span data-stu-id="c4645-135">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="c4645-136">Name the resource group **myResourceGroup** and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4645-136">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="c4645-137">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="c4645-137">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="c4645-138">Next to **Hosting Plan**, select **New**.</span><span class="sxs-lookup"><span data-stu-id="c4645-138">Next to **Hosting Plan**, select **New**.</span></span> 

<span data-ttu-id="c4645-139">In the **Configure Hosting Plan** dialog, use the settings in the table following the screenshot.</span><span class="sxs-lookup"><span data-stu-id="c4645-139">In the **Configure Hosting Plan** dialog, use the settings in the table following the screenshot.</span></span>

![Create App Service plan](./media/app-service-web-get-started-dotnet-framework/configure-app-service-plan.png)

| <span data-ttu-id="c4645-141">Setting</span><span class="sxs-lookup"><span data-stu-id="c4645-141">Setting</span></span> | <span data-ttu-id="c4645-142">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="c4645-142">Suggested Value</span></span> | <span data-ttu-id="c4645-143">Description</span><span class="sxs-lookup"><span data-stu-id="c4645-143">Description</span></span> |
|-|-|-|
|<span data-ttu-id="c4645-144">App Service Plan</span><span class="sxs-lookup"><span data-stu-id="c4645-144">App Service Plan</span></span>| <span data-ttu-id="c4645-145">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c4645-145">myAppServicePlan</span></span> | <span data-ttu-id="c4645-146">Name of the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c4645-146">Name of the App Service plan.</span></span> |
| <span data-ttu-id="c4645-147">Location</span><span class="sxs-lookup"><span data-stu-id="c4645-147">Location</span></span> | <span data-ttu-id="c4645-148">West Europe</span><span class="sxs-lookup"><span data-stu-id="c4645-148">West Europe</span></span> | <span data-ttu-id="c4645-149">The datacenter where the web app is hosted.</span><span class="sxs-lookup"><span data-stu-id="c4645-149">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="c4645-150">Size</span><span class="sxs-lookup"><span data-stu-id="c4645-150">Size</span></span> | <span data-ttu-id="c4645-151">Free</span><span class="sxs-lookup"><span data-stu-id="c4645-151">Free</span></span> | <span data-ttu-id="c4645-152">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) determines hosting features.</span><span class="sxs-lookup"><span data-stu-id="c4645-152">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) determines hosting features.</span></span> |

<span data-ttu-id="c4645-153">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4645-153">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="c4645-154">Create and publish the web app</span><span class="sxs-lookup"><span data-stu-id="c4645-154">Create and publish the web app</span></span>

<span data-ttu-id="c4645-155">In **App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span><span class="sxs-lookup"><span data-stu-id="c4645-155">In **App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="c4645-156">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your app name.</span><span class="sxs-lookup"><span data-stu-id="c4645-156">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your app name.</span></span>

<span data-ttu-id="c4645-157">Select **Create** to start creating the Azure resources.</span><span class="sxs-lookup"><span data-stu-id="c4645-157">Select **Create** to start creating the Azure resources.</span></span>

![Configure app name](./media/app-service-web-get-started-dotnet-framework/web-app-name.png)

<span data-ttu-id="c4645-159">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span><span class="sxs-lookup"><span data-stu-id="c4645-159">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![Published ASP.NET web app in Azure](./media/app-service-web-get-started-dotnet-framework/published-azure-web-app.png)

<span data-ttu-id="c4645-161">The app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c4645-161">The app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="c4645-162">Congratulations, your ASP.NET web app is running live in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c4645-162">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="c4645-163">Update the app and redeploy</span><span class="sxs-lookup"><span data-stu-id="c4645-163">Update the app and redeploy</span></span>

<span data-ttu-id="c4645-164">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="c4645-164">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="c4645-165">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span><span class="sxs-lookup"><span data-stu-id="c4645-165">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="c4645-166">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c4645-166">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="c4645-167">On the publish page, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c4645-167">On the publish page, select **Publish**.</span></span>
<span data-ttu-id="c4645-168">![Visual Studio publish summary page](./media/app-service-web-get-started-dotnet-framework/publish-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="c4645-168">![Visual Studio publish summary page](./media/app-service-web-get-started-dotnet-framework/publish-summary-page.png)</span></span>

<span data-ttu-id="c4645-169">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span><span class="sxs-lookup"><span data-stu-id="c4645-169">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Updated ASP.NET web app in Azure](./media/app-service-web-get-started-dotnet-framework/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="c4645-171">Manage the Azure web app</span><span class="sxs-lookup"><span data-stu-id="c4645-171">Manage the Azure web app</span></span>

<span data-ttu-id="c4645-172">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span><span class="sxs-lookup"><span data-stu-id="c4645-172">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="c4645-173">From the left menu, select **App Services**, and then select the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c4645-173">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-get-started-dotnet-framework/access-portal.png)

<span data-ttu-id="c4645-175">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="c4645-175">You see your web app's Overview page.</span></span> <span data-ttu-id="c4645-176">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="c4645-176">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service blade in Azure portal](./media/app-service-web-get-started-dotnet-framework/web-app-blade.png)

<span data-ttu-id="c4645-178">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="c4645-178">The left menu provides different pages for configuring your app.</span></span> 

## <a name="video"></a><span data-ttu-id="c4645-179">Video</span><span class="sxs-lookup"><span data-stu-id="c4645-179">Video</span></span>

<span data-ttu-id="c4645-180">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span><span class="sxs-lookup"><span data-stu-id="c4645-180">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="c4645-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4645-181">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4645-182">ASP.NET with SQL Database</span><span class="sxs-lookup"><span data-stu-id="c4645-182">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
