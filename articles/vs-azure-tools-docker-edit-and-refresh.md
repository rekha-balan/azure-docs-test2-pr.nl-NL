---
title: Debugging apps in a local Docker container | Microsoft Docs
description: Learn how to modify an app that is running in a local Docker container, refresh the container via Edit and Refresh and set debugging breakpoints
services: azure-container-service
documentationcenter: na
author: ghogen
manager: douge
editor: ''
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: 07a7c1e11d8ca20ff4f42abcb84961cb7cd9e0e1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809561"
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="1826a-103">Debugging apps in a local Docker container</span><span class="sxs-lookup"><span data-stu-id="1826a-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="1826a-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1826a-104">Overview</span></span>
<span data-ttu-id="1826a-105">Visual Studio 2017 provides a consistent way to develop in a Linux Docker container and validate your application locally.</span><span class="sxs-lookup"><span data-stu-id="1826a-105">Visual Studio 2017 provides a consistent way to develop in a Linux Docker container and validate your application locally.</span></span>
<span data-ttu-id="1826a-106">You don't have to restart the container each time you make a code change.</span><span class="sxs-lookup"><span data-stu-id="1826a-106">You don't have to restart the container each time you make a code change.</span></span>
<span data-ttu-id="1826a-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span><span class="sxs-lookup"><span data-stu-id="1826a-107">This article illustrates how to use the "Edit and Refresh" feature to start an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh the browser to see those changes.</span></span>
<span data-ttu-id="1826a-108">This article also shows you how to set breakpoints for debugging.</span><span class="sxs-lookup"><span data-stu-id="1826a-108">This article also shows you how to set breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="1826a-109">Windows Container support will be coming in a future release</span><span class="sxs-lookup"><span data-stu-id="1826a-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="1826a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1826a-110">Prerequisites</span></span>
<span data-ttu-id="1826a-111">The following tools must be installed.</span><span class="sxs-lookup"><span data-stu-id="1826a-111">The following tools must be installed.</span></span>

* [<span data-ttu-id="1826a-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1826a-112">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="1826a-113">Microsoft ASP.NET Core 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="1826a-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="1826a-114">To run Docker containers locally, you'll need a local docker client.</span><span class="sxs-lookup"><span data-stu-id="1826a-114">To run Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="1826a-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1826a-115">You can use the [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V to be disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="1826a-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="1826a-116">If using Docker Toolbox, you'll need to [configure the Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="1826a-117">1. Create a web app</span><span class="sxs-lookup"><span data-stu-id="1826a-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="1826a-118">2. Add Docker support</span><span class="sxs-lookup"><span data-stu-id="1826a-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="1826a-119">3. Edit your code and refresh</span><span class="sxs-lookup"><span data-stu-id="1826a-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="1826a-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span><span class="sxs-lookup"><span data-stu-id="1826a-120">To quickly iterate changes, you can start your application within a container, and continue to make changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="1826a-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span><span class="sxs-lookup"><span data-stu-id="1826a-121">Set the Solution Configuration to `Debug` and press **&lt;CTRL + F5>** to build your docker image and run it locally.</span></span>

    <span data-ttu-id="1826a-122">Once the container image has been built and is running in a Docker container, Visual Studio launches the Web app in your default browser.</span><span class="sxs-lookup"><span data-stu-id="1826a-122">Once the container image has been built and is running in a Docker container, Visual Studio launches the Web app in your default browser.</span></span>
    <span data-ttu-id="1826a-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span><span class="sxs-lookup"><span data-stu-id="1826a-123">If you are using the Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="1826a-124">Go to the About page, which is where we're going to make our changes.</span><span class="sxs-lookup"><span data-stu-id="1826a-124">Go to the About page, which is where we're going to make our changes.</span></span>
3. <span data-ttu-id="1826a-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="1826a-125">Return to Visual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="1826a-126">Add the following HTML content to the end of the file and save the changes.</span><span class="sxs-lookup"><span data-stu-id="1826a-126">Add the following HTML content to the end of the file and save the changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="1826a-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span><span class="sxs-lookup"><span data-stu-id="1826a-127">Viewing the output window, when the .NET build is completed and you see these lines, switch back to your browser and refresh the About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C to shut down
   ```
6. <span data-ttu-id="1826a-128">Your changes have been applied!</span><span class="sxs-lookup"><span data-stu-id="1826a-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="1826a-129">4. Debug with breakpoints</span><span class="sxs-lookup"><span data-stu-id="1826a-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="1826a-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1826a-130">Often, changes will need further inspection, leveraging the debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="1826a-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="1826a-131">Return to Visual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="1826a-132">Replace the contents of the About() method with the following:</span><span class="sxs-lookup"><span data-stu-id="1826a-132">Replace the contents of the About() method with the following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="1826a-133">Set a breakpoint to the left of the `string message`... line.</span><span class="sxs-lookup"><span data-stu-id="1826a-133">Set a breakpoint to the left of the `string message`... line.</span></span>
4. <span data-ttu-id="1826a-134">Hit **&lt;F5>** to start debugging.</span><span class="sxs-lookup"><span data-stu-id="1826a-134">Hit **&lt;F5>** to start debugging.</span></span>
5. <span data-ttu-id="1826a-135">Navigate to the About page to hit your breakpoint.</span><span class="sxs-lookup"><span data-stu-id="1826a-135">Navigate to the About page to hit your breakpoint.</span></span>
6. <span data-ttu-id="1826a-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span><span class="sxs-lookup"><span data-stu-id="1826a-136">Switch to Visual Studio to view the breakpoint, and inspect the value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="1826a-137">Summary</span><span class="sxs-lookup"><span data-stu-id="1826a-137">Summary</span></span>
<span data-ttu-id="1826a-138">With Docker support in Visual Studio 2017, you can get the productivity of working locally, with the production realism of developing within a Docker container.</span><span class="sxs-lookup"><span data-stu-id="1826a-138">With Docker support in Visual Studio 2017, you can get the productivity of working locally, with the production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="1826a-139">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="1826a-139">Troubleshooting</span></span>
[<span data-ttu-id="1826a-140">Troubleshooting Visual Studio Docker Development</span><span class="sxs-lookup"><span data-stu-id="1826a-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="1826a-141">More about Docker with Visual Studio, Windows, and Azure</span><span class="sxs-lookup"><span data-stu-id="1826a-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="1826a-142">[Docker Tools for Azure DevOps](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span><span class="sxs-lookup"><span data-stu-id="1826a-142">[Docker Tools for Azure DevOps](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="1826a-143">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span><span class="sxs-lookup"><span data-stu-id="1826a-143">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="1826a-144">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span><span class="sxs-lookup"><span data-stu-id="1826a-144">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="1826a-145">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="1826a-145">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="1826a-146">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="1826a-146">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="1826a-147">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="1826a-147">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="1826a-148">Various Docker tools</span><span class="sxs-lookup"><span data-stu-id="1826a-148">Various Docker tools</span></span>
[<span data-ttu-id="1826a-149">Some great docker tools (Steve Lasker's blog)</span><span class="sxs-lookup"><span data-stu-id="1826a-149">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="1826a-150">Good articles</span><span class="sxs-lookup"><span data-stu-id="1826a-150">Good articles</span></span>
[<span data-ttu-id="1826a-151">Introduction to Microservices from NGINX</span><span class="sxs-lookup"><span data-stu-id="1826a-151">Introduction to Microservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="1826a-152">Presentations</span><span class="sxs-lookup"><span data-stu-id="1826a-152">Presentations</span></span>
* [<span data-ttu-id="1826a-153">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="1826a-153">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="1826a-154">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span><span class="sxs-lookup"><span data-stu-id="1826a-154">Introduction to ASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="1826a-155">Developing .NET apps in containers, Channel 9</span><span class="sxs-lookup"><span data-stu-id="1826a-155">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
