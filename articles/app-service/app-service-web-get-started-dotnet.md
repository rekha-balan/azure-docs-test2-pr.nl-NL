---
title: Create a C# ASP.NET Core web app in Azure | Microsoft Docs
description: Learn how to run web apps in Azure App Service by deploying the default C# ASP.NET web app.
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/05/2018
ms.author: cephalin
ms.custom: mvc, devcenter, vs-azure
ms.openlocfilehash: 00a1f7edfb24d9bd44e48161f3cd2e69cba36bfc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855816"
---
# <a name="create-an-aspnet-core-web-app-in-azure"></a><span data-ttu-id="f4e4c-103">Create an ASP.NET Core web app in Azure</span><span class="sxs-lookup"><span data-stu-id="f4e4c-103">Create an ASP.NET Core web app in Azure</span></span>

> [!NOTE]
> <span data-ttu-id="f4e4c-104">This article deploys an app to App Service on Windows.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-104">This article deploys an app to App Service on Windows.</span></span> <span data-ttu-id="f4e4c-105">To deploy to App Service on _Linux_, see [Create a .NET Core web app in App Service on Linux](./containers/quickstart-dotnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="f4e4c-105">To deploy to App Service on _Linux_, see [Create a .NET Core web app in App Service on Linux](./containers/quickstart-dotnetcore.md).</span></span>
>

<span data-ttu-id="f4e4c-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-106">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="f4e4c-107">This quickstart shows how to deploy your first ASP.NET Core web app to Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-107">This quickstart shows how to deploy your first ASP.NET Core web app to Azure Web Apps.</span></span> <span data-ttu-id="f4e4c-108">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-108">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

![](./media/app-service-web-get-started-dotnet/web-app-running-live.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="f4e4c-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4e4c-109">Prerequisites</span></span>

<span data-ttu-id="f4e4c-110">To complete this tutorial, install <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> with the **ASP.NET and web development** workload.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-110">To complete this tutorial, install <a href="https://www.visualstudio.com/downloads/" target="_blank">Visual Studio 2017</a> with the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="f4e4c-111">If you've installed Visual Studio 2017 already:</span><span class="sxs-lookup"><span data-stu-id="f4e4c-111">If you've installed Visual Studio 2017 already:</span></span>

- <span data-ttu-id="f4e4c-112">Install the latest updates in Visual Studio by clicking **Help** > **Check for Updates**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-112">Install the latest updates in Visual Studio by clicking **Help** > **Check for Updates**.</span></span>
- <span data-ttu-id="f4e4c-113">Add the workload by clicking **Tools** > **Get Tools and Features**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-113">Add the workload by clicking **Tools** > **Get Tools and Features**.</span></span>

## <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="f4e4c-114">Create an ASP.NET Core web app</span><span class="sxs-lookup"><span data-stu-id="f4e4c-114">Create an ASP.NET Core web app</span></span>

<span data-ttu-id="f4e4c-115">In Visual Studio, create a project by selecting **File > New > Project**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="f4e4c-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Core Web Application**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Core Web Application**.</span></span>

<span data-ttu-id="f4e4c-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![New Project dialog box](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="f4e4c-119">You can deploy any type of ASP.NET Core web app to Azure.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-119">You can deploy any type of ASP.NET Core web app to Azure.</span></span> <span data-ttu-id="f4e4c-120">For this quickstart, select the **Web Application** template, and make sure authentication is set to **No Authentication** and no other option is selected.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-120">For this quickstart, select the **Web Application** template, and make sure authentication is set to **No Authentication** and no other option is selected.</span></span>
      
<span data-ttu-id="f4e4c-121">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-121">Select **OK**.</span></span>

![New ASP.NET Project dialog box](./media/app-service-web-get-started-dotnet/razor-pages-aspnet-dialog.png)

<span data-ttu-id="f4e4c-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Run app locally](./media/app-service-web-get-started-dotnet/razor-web-app-running-locally.png)

## <a name="launch-the-publish-wizard"></a><span data-ttu-id="f4e4c-125">Launch the publish wizard</span><span class="sxs-lookup"><span data-stu-id="f4e4c-125">Launch the publish wizard</span></span>

<span data-ttu-id="f4e4c-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publish from Solution Explorer](./media/app-service-web-get-started-dotnet/right-click-publish.png)

<span data-ttu-id="f4e4c-128">The publish wizard is automatically launched.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-128">The publish wizard is automatically launched.</span></span> <span data-ttu-id="f4e4c-129">Select **App Service** > **Publish** to open the **Create App Service** dialog.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-129">Select **App Service** > **Publish** to open the **Create App Service** dialog.</span></span>

![Publish from project overview page](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

## <a name="sign-in-to-azure"></a><span data-ttu-id="f4e4c-131">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="f4e4c-131">Sign in to Azure</span></span>

<span data-ttu-id="f4e4c-132">In the **Create App Service** dialog, click **Add an account**, and sign in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-132">In the **Create App Service** dialog, click **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="f4e4c-133">If you're already signed in, select the account you want from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-133">If you're already signed in, select the account you want from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="f4e4c-134">If you're already signed in, don't select **Create** yet.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-134">If you're already signed in, don't select **Create** yet.</span></span>
>
   
![Sign in to Azure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="f4e4c-136">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f4e4c-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="f4e4c-137">Next to **Resource Group**, select **New**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="f4e4c-138">Name the resource group **myResourceGroup** and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="f4e4c-139">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="f4e4c-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="f4e4c-140">Next to **Hosting Plan**, select **New**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-140">Next to **Hosting Plan**, select **New**.</span></span> 

<span data-ttu-id="f4e4c-141">In the **Configure Hosting Plan** dialog, use the settings in the table following the screenshot.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-141">In the **Configure Hosting Plan** dialog, use the settings in the table following the screenshot.</span></span>

![Create App Service plan](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="f4e4c-143">Setting</span><span class="sxs-lookup"><span data-stu-id="f4e4c-143">Setting</span></span> | <span data-ttu-id="f4e4c-144">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="f4e4c-144">Suggested Value</span></span> | <span data-ttu-id="f4e4c-145">Description</span><span class="sxs-lookup"><span data-stu-id="f4e4c-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="f4e4c-146">App Service Plan</span><span class="sxs-lookup"><span data-stu-id="f4e4c-146">App Service Plan</span></span>| <span data-ttu-id="f4e4c-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f4e4c-147">myAppServicePlan</span></span> | <span data-ttu-id="f4e4c-148">Name of the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="f4e4c-149">Location</span><span class="sxs-lookup"><span data-stu-id="f4e4c-149">Location</span></span> | <span data-ttu-id="f4e4c-150">West Europe</span><span class="sxs-lookup"><span data-stu-id="f4e4c-150">West Europe</span></span> | <span data-ttu-id="f4e4c-151">The datacenter where the web app is hosted.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="f4e4c-152">Size</span><span class="sxs-lookup"><span data-stu-id="f4e4c-152">Size</span></span> | <span data-ttu-id="f4e4c-153">Free</span><span class="sxs-lookup"><span data-stu-id="f4e4c-153">Free</span></span> | <span data-ttu-id="f4e4c-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) determines hosting features.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) determines hosting features.</span></span> |

<span data-ttu-id="f4e4c-155">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="f4e4c-156">Create and publish the web app</span><span class="sxs-lookup"><span data-stu-id="f4e4c-156">Create and publish the web app</span></span>

<span data-ttu-id="f4e4c-157">In **App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-157">In **App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="f4e4c-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your app name.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your app name.</span></span>

<span data-ttu-id="f4e4c-159">Select **Create** to start creating the Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-159">Select **Create** to start creating the Azure resources.</span></span>

![Configure app name](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="f4e4c-161">Once the wizard completes, it publishes the ASP.NET Core web app to Azure, and then launches the app in the default browser.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-161">Once the wizard completes, it publishes the ASP.NET Core web app to Azure, and then launches the app in the default browser.</span></span>

![Published ASP.NET web app in Azure](./media/app-service-web-get-started-dotnet/web-app-running-live.png)

<span data-ttu-id="f4e4c-163">The app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-163">The app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="f4e4c-164">Congratulations, your ASP.NET Core web app is running live in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-164">Congratulations, your ASP.NET Core web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="f4e4c-165">Update the app and redeploy</span><span class="sxs-lookup"><span data-stu-id="f4e4c-165">Update the app and redeploy</span></span>

<span data-ttu-id="f4e4c-166">From the **Solution Explorer**, open _Pages/Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-166">From the **Solution Explorer**, open _Pages/Index.cshtml_.</span></span>

<span data-ttu-id="f4e4c-167">Replace the two `<div>` tags with the following code:</span><span class="sxs-lookup"><span data-stu-id="f4e4c-167">Replace the two `<div>` tags with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="f4e4c-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="f4e4c-169">In the publish summary page, select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-169">In the publish summary page, select **Publish**.</span></span>
<span data-ttu-id="f4e4c-170">![Visual Studio publish summary page](./media/app-service-web-get-started-dotnet/publish-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="f4e4c-170">![Visual Studio publish summary page](./media/app-service-web-get-started-dotnet/publish-summary-page.png)</span></span>

<span data-ttu-id="f4e4c-171">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-171">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Updated ASP.NET web app in Azure](./media/app-service-web-get-started-dotnet/web-app-running-live-updated.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="f4e4c-173">Manage the Azure web app</span><span class="sxs-lookup"><span data-stu-id="f4e4c-173">Manage the Azure web app</span></span>

<span data-ttu-id="f4e4c-174">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-174">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="f4e4c-175">From the left menu, select **App Services**, and then select the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-175">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="f4e4c-177">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-177">You see your web app's Overview page.</span></span> <span data-ttu-id="f4e4c-178">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-178">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service blade in Azure portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="f4e4c-180">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="f4e4c-180">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="f4e4c-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4e4c-181">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f4e4c-182">ASP.NET Core with SQL Database</span><span class="sxs-lookup"><span data-stu-id="f4e4c-182">ASP.NET Core with SQL Database</span></span>](app-service-web-tutorial-dotnetcore-sqldb.md)
