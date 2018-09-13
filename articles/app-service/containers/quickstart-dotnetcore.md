---
title: Create a .NET Core web app and deploy to App Service on Linux | Microsoft Docs
description: Deploy your first .NET Core Hello World app to App Service on Linux in minutes.
keywords: azure app service, web app, dotnet, core, linux, oss
services: app-service
documentationCenter: ''
author: cephalin
manager: syntaxc4
editor: ''
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: quickstart
ms.date: 04/11/2018
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1345d4c4d349ed2fa5bb95ee35299c77fb391359
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856030"
---
# <a name="create-a-net-core-web-app-in-app-service-on-linux"></a><span data-ttu-id="12777-104">Create a .NET Core web app in App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="12777-104">Create a .NET Core web app in App Service on Linux</span></span>

> [!NOTE]
> <span data-ttu-id="12777-105">This article deploys an app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="12777-105">This article deploys an app to App Service on Linux.</span></span> <span data-ttu-id="12777-106">To deploy to App Service on _Windows_, see [Create an ASP.NET Core web app in Azure](../app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="12777-106">To deploy to App Service on _Windows_, see [Create an ASP.NET Core web app in Azure](../app-service-web-get-started-dotnet.md).</span></span>
>

<span data-ttu-id="12777-107">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span><span class="sxs-lookup"><span data-stu-id="12777-107">[App Service on Linux](app-service-linux-intro.md) provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="12777-108">This quickstart shows how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="12777-108">This quickstart shows how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on App Service on Linux.</span></span> <span data-ttu-id="12777-109">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy the .NET Core code to the web app.</span><span class="sxs-lookup"><span data-stu-id="12777-109">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy the .NET Core code to the web app.</span></span>

![Sample app running in Azure](media/quickstart-dotnetcore/dotnet-browse-azure.png)

<span data-ttu-id="12777-111">You can follow the steps in this article using a Mac, Windows, or Linux machine.</span><span class="sxs-lookup"><span data-stu-id="12777-111">You can follow the steps in this article using a Mac, Windows, or Linux machine.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="12777-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="12777-112">Prerequisites</span></span>

<span data-ttu-id="12777-113">To complete this quickstart:</span><span class="sxs-lookup"><span data-stu-id="12777-113">To complete this quickstart:</span></span>

* <span data-ttu-id="12777-114"><a href="https://git-scm.com/" target="_blank">Install Git</a></span><span class="sxs-lookup"><span data-stu-id="12777-114"><a href="https://git-scm.com/" target="_blank">Install Git</a></span></span>
* <span data-ttu-id="12777-115"><a href="https://www.microsoft.com/net/core/" target="_blank">Install .NET Core</a></span><span class="sxs-lookup"><span data-stu-id="12777-115"><a href="https://www.microsoft.com/net/core/" target="_blank">Install .NET Core</a></span></span>

## <a name="create-the-app-locally"></a><span data-ttu-id="12777-116">Create the app locally</span><span class="sxs-lookup"><span data-stu-id="12777-116">Create the app locally</span></span>

<span data-ttu-id="12777-117">In a terminal window on your machine, create a directory named `hellodotnetcore` and change the current directory to it.</span><span class="sxs-lookup"><span data-stu-id="12777-117">In a terminal window on your machine, create a directory named `hellodotnetcore` and change the current directory to it.</span></span>

```bash
md hellodotnetcore
cd hellodotnetcore
```

<span data-ttu-id="12777-118">Create a new .NET Core web app.</span><span class="sxs-lookup"><span data-stu-id="12777-118">Create a new .NET Core web app.</span></span>

```bash
dotnet new web
```

## <a name="run-the-app-locally"></a><span data-ttu-id="12777-119">Run the app locally</span><span class="sxs-lookup"><span data-stu-id="12777-119">Run the app locally</span></span>

<span data-ttu-id="12777-120">Run the application locally so that you see how it should look when you deploy it to Azure.</span><span class="sxs-lookup"><span data-stu-id="12777-120">Run the application locally so that you see how it should look when you deploy it to Azure.</span></span> 

<span data-ttu-id="12777-121">Restore the NuGet packages and run the app.</span><span class="sxs-lookup"><span data-stu-id="12777-121">Restore the NuGet packages and run the app.</span></span>

```bash
dotnet restore
dotnet run
```

<span data-ttu-id="12777-122">Open a web browser, and navigate to the app at `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="12777-122">Open a web browser, and navigate to the app at `http://localhost:5000`.</span></span>

<span data-ttu-id="12777-123">You see the **Hello World** message from the sample app displayed in the page.</span><span class="sxs-lookup"><span data-stu-id="12777-123">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![Test with browser](media/quickstart-dotnetcore/dotnet-browse-local.png)

<span data-ttu-id="12777-125">In your terminal window, press **Ctrl+C** to exit the web server.</span><span class="sxs-lookup"><span data-stu-id="12777-125">In your terminal window, press **Ctrl+C** to exit the web server.</span></span> <span data-ttu-id="12777-126">Initialize a Git repository for the .NET Core project.</span><span class="sxs-lookup"><span data-stu-id="12777-126">Initialize a Git repository for the .NET Core project.</span></span>

```bash
git init
git add .
git commit -m "first commit"
```

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../../includes/app-service-web-create-resource-group-linux.md)]

[!INCLUDE [Create app service plan](../../../includes/app-service-web-create-app-service-plan-linux.md)]

## <a name="create-a-web-app"></a><span data-ttu-id="12777-127">Create a web app</span><span class="sxs-lookup"><span data-stu-id="12777-127">Create a web app</span></span>

[!INCLUDE [Create web app](../../../includes/app-service-web-create-web-app-dotnetcore-linux-no-h.md)]

<span data-ttu-id="12777-128">Browse to your newly created web app.</span><span class="sxs-lookup"><span data-stu-id="12777-128">Browse to your newly created web app.</span></span> <span data-ttu-id="12777-129">Replace _&lt;app name>_ with your web app name.</span><span class="sxs-lookup"><span data-stu-id="12777-129">Replace _&lt;app name>_ with your web app name.</span></span>

```bash
http://<app name>.azurewebsites.net
```

<span data-ttu-id="12777-130">Here is what your new web app should look like:</span><span class="sxs-lookup"><span data-stu-id="12777-130">Here is what your new web app should look like:</span></span>

![Empty web app page](media/quickstart-dotnetcore/dotnet-browse-created.png)

[!INCLUDE [Push to Azure](../../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 22, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (18/18), done.
Writing objects: 100% (22/22), 51.21 KiB | 3.94 MiB/s, done.
Total 22 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '741f16d1db'.
remote: Generating deployment script.
remote: Project file path: ./hellodotnetcore.csproj
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling ASP.NET Core Web Application deployment.
remote: ...............................................................................................
remote:   Restoring packages for /home/site/repository/hellodotnetcore.csproj...
remote: ....................................
remote:   Installing System.Xml.XPath 4.0.1.
remote:   Installing System.Diagnostics.Tracing 4.1.0.
remote:   Installing System.Threading.Tasks.Extensions 4.0.0.
remote:   Installing System.Reflection.Emit.ILGeneration 4.0.1.
remote:   ...
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://cephalin-dotnetcore.scm.azurewebsites.net/cephalin-dotnetcore.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="12777-132">Browse to the app</span><span class="sxs-lookup"><span data-stu-id="12777-132">Browse to the app</span></span>

<span data-ttu-id="12777-133">Browse to the deployed application using your web browser.</span><span class="sxs-lookup"><span data-stu-id="12777-133">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="12777-134">The .NET Core sample code is running in a web app with a built-in image.</span><span class="sxs-lookup"><span data-stu-id="12777-134">The .NET Core sample code is running in a web app with a built-in image.</span></span>

![Sample app running in Azure](media/quickstart-dotnetcore/dotnet-browse-azure.png)

<span data-ttu-id="12777-136">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="12777-136">**Congratulations!**</span></span> <span data-ttu-id="12777-137">You've deployed your first .NET Core app to App Service on Linux.</span><span class="sxs-lookup"><span data-stu-id="12777-137">You've deployed your first .NET Core app to App Service on Linux.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="12777-138">Update and redeploy the code</span><span class="sxs-lookup"><span data-stu-id="12777-138">Update and redeploy the code</span></span>

<span data-ttu-id="12777-139">In the local directory, open the _Startup.cs_ file.</span><span class="sxs-lookup"><span data-stu-id="12777-139">In the local directory, open the _Startup.cs_ file.</span></span> <span data-ttu-id="12777-140">Make a small change to the text in the method call `context.Response.WriteAsync`:</span><span class="sxs-lookup"><span data-stu-id="12777-140">Make a small change to the text in the method call `context.Response.WriteAsync`:</span></span>

```csharp
await context.Response.WriteAsync("Hello Azure!");
```

<span data-ttu-id="12777-141">Commit your changes in Git, and then push the code changes to Azure.</span><span class="sxs-lookup"><span data-stu-id="12777-141">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="12777-142">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span><span class="sxs-lookup"><span data-stu-id="12777-142">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![Updated sample app running in Azure](media/quickstart-dotnetcore/dotnet-browse-azure-updated.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="12777-144">Manage your new Azure web app</span><span class="sxs-lookup"><span data-stu-id="12777-144">Manage your new Azure web app</span></span>

<span data-ttu-id="12777-145">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span><span class="sxs-lookup"><span data-stu-id="12777-145">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="12777-146">From the left menu, click **App Services**, and then click the name of your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="12777-146">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portal navigation to Azure web app](./media/quickstart-dotnetcore/portal-app-service-list.png)

<span data-ttu-id="12777-148">You see your web app's Overview page.</span><span class="sxs-lookup"><span data-stu-id="12777-148">You see your web app's Overview page.</span></span> <span data-ttu-id="12777-149">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span><span class="sxs-lookup"><span data-stu-id="12777-149">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![App Service page in Azure portal](media/quickstart-dotnetcore/portal-app-overview.png)

<span data-ttu-id="12777-151">The left menu provides different pages for configuring your app.</span><span class="sxs-lookup"><span data-stu-id="12777-151">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="12777-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="12777-152">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="12777-153">Build a .NET Core and SQL Database web app in Azure App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="12777-153">Build a .NET Core and SQL Database web app in Azure App Service on Linux</span></span>](tutorial-dotnetcore-sqldb-app.md)
