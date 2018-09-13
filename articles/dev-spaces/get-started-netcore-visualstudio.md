---
title: Create a Kubernetes dev space in the cloud using .NET Core and Visual Studio | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.custom: vs-azure
ms.workload: azure-vs
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 07/09/2018
ms.topic: tutorial
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: douge
ms.openlocfilehash: ac1872cf3f5ee8b83da9fa4c489188504aa8ad22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870289"
---
# <a name="get-started-on-azure-dev-spaces-with-net-core-and-visual-studio"></a><span data-ttu-id="cb414-104">Get Started on Azure Dev Spaces with .NET Core and Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb414-104">Get Started on Azure Dev Spaces with .NET Core and Visual Studio</span></span>

<span data-ttu-id="cb414-105">In this guide, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="cb414-105">In this guide, you will learn how to:</span></span>

- <span data-ttu-id="cb414-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb414-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span></span>
- <span data-ttu-id="cb414-107">Iteratively develop code in containers using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb414-107">Iteratively develop code in containers using Visual Studio.</span></span>
- <span data-ttu-id="cb414-108">Independently develop two separate services, and used Kubernetes' DNS service discovery to make a call to another service.</span><span class="sxs-lookup"><span data-stu-id="cb414-108">Independently develop two separate services, and used Kubernetes' DNS service discovery to make a call to another service.</span></span>
- <span data-ttu-id="cb414-109">Productively develop and test your code in a team environment.</span><span class="sxs-lookup"><span data-stu-id="cb414-109">Productively develop and test your code in a team environment.</span></span>

[!INCLUDE [](includes/see-troubleshooting.md)]

[!INCLUDE [](includes/portal-aks-cluster.md)]

## <a name="get-the-visual-studio-tools"></a><span data-ttu-id="cb414-110">Get the Visual Studio tools</span><span class="sxs-lookup"><span data-stu-id="cb414-110">Get the Visual Studio tools</span></span>
1. <span data-ttu-id="cb414-111">Install the latest version of [Visual Studio 2017](https://www.visualstudio.com/vs/)</span><span class="sxs-lookup"><span data-stu-id="cb414-111">Install the latest version of [Visual Studio 2017](https://www.visualstudio.com/vs/)</span></span>
1. <span data-ttu-id="cb414-112">In the Visual Studio installer make sure the following Workload is selected:</span><span class="sxs-lookup"><span data-stu-id="cb414-112">In the Visual Studio installer make sure the following Workload is selected:</span></span>
    * <span data-ttu-id="cb414-113">ASP.NET and web development</span><span class="sxs-lookup"><span data-stu-id="cb414-113">ASP.NET and web development</span></span>
1. <span data-ttu-id="cb414-114">Install [Visual Studio Tools for Kubernetes](https://aka.ms/get-azds-visualstudio)</span><span class="sxs-lookup"><span data-stu-id="cb414-114">Install [Visual Studio Tools for Kubernetes](https://aka.ms/get-azds-visualstudio)</span></span>

## <a name="create-a-web-app-running-in-a-container"></a><span data-ttu-id="cb414-115">Create a web app running in a container</span><span class="sxs-lookup"><span data-stu-id="cb414-115">Create a web app running in a container</span></span>

<span data-ttu-id="cb414-116">In this section, you'll create a ASP.NET Core web app and get it running in a container in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="cb414-116">In this section, you'll create a ASP.NET Core web app and get it running in a container in Kubernetes.</span></span>

### <a name="create-an-aspnet-web-app"></a><span data-ttu-id="cb414-117">Create an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="cb414-117">Create an ASP.NET web app</span></span>

<span data-ttu-id="cb414-118">From within Visual Studio 2017, create a new project.</span><span class="sxs-lookup"><span data-stu-id="cb414-118">From within Visual Studio 2017, create a new project.</span></span> <span data-ttu-id="cb414-119">Currently, the project must be an **ASP.NET Core Web Application**.</span><span class="sxs-lookup"><span data-stu-id="cb414-119">Currently, the project must be an **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="cb414-120">Name the project '**webfrontend**'.</span><span class="sxs-lookup"><span data-stu-id="cb414-120">Name the project '**webfrontend**'.</span></span>

![](media/get-started-netcore-visualstudio/NewProjectDialog1.png)

<span data-ttu-id="cb414-121">Select the **Web Application (Model-View-Controller)** template and be sure you're targeting **.NET Core** and **ASP.NET Core 2.0** in the two dropdowns at the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cb414-121">Select the **Web Application (Model-View-Controller)** template and be sure you're targeting **.NET Core** and **ASP.NET Core 2.0** in the two dropdowns at the top of the dialog.</span></span> <span data-ttu-id="cb414-122">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="cb414-122">Click **OK** to create the project.</span></span>

![](media/get-started-netcore-visualstudio/NewProjectDialog2.png)


### <a name="enable-dev-spaces-for-an-aks-cluster"></a><span data-ttu-id="cb414-123">Enable Dev Spaces for an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="cb414-123">Enable Dev Spaces for an AKS cluster</span></span>

<span data-ttu-id="cb414-124">With the project you just created, select **Azure Dev Spaces** from the launch settings dropdown, as shown below.</span><span class="sxs-lookup"><span data-stu-id="cb414-124">With the project you just created, select **Azure Dev Spaces** from the launch settings dropdown, as shown below.</span></span>

![](media/get-started-netcore-visualstudio/LaunchSettings.png)

<span data-ttu-id="cb414-125">In the dialog that is displayed next, make sure you are signed in with the appropriate account, and then either select an existing Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="cb414-125">In the dialog that is displayed next, make sure you are signed in with the appropriate account, and then either select an existing Kubernetes cluster.</span></span>

![](media/get-started-netcore-visualstudio/Azure-Dev-Spaces-Dialog.PNG)

<span data-ttu-id="cb414-126">Leave the **Space** dropdown defaulted to `default` for now.</span><span class="sxs-lookup"><span data-stu-id="cb414-126">Leave the **Space** dropdown defaulted to `default` for now.</span></span> <span data-ttu-id="cb414-127">Later, you'll learn more about this option.</span><span class="sxs-lookup"><span data-stu-id="cb414-127">Later, you'll learn more about this option.</span></span> <span data-ttu-id="cb414-128">Check the **Publicly Accessible** checkbox so the web app will be accessible via a public endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb414-128">Check the **Publicly Accessible** checkbox so the web app will be accessible via a public endpoint.</span></span> <span data-ttu-id="cb414-129">This setting isn't required, but it will be helpful to demonstrate some concepts later in this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="cb414-129">This setting isn't required, but it will be helpful to demonstrate some concepts later in this walkthrough.</span></span> <span data-ttu-id="cb414-130">But don’t worry, in either case you will be able to debug your website using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb414-130">But don’t worry, in either case you will be able to debug your website using Visual Studio.</span></span>

![](media/get-started-netcore-visualstudio/Azure-Dev-Spaces-Dialog2.png)

<span data-ttu-id="cb414-131">Click **OK** to select or create the cluster.</span><span class="sxs-lookup"><span data-stu-id="cb414-131">Click **OK** to select or create the cluster.</span></span>

<span data-ttu-id="cb414-132">If you choose a cluster that hasn't been enabled to work with Azure Dev Spaces, you'll see a message asking if you want to configure it.</span><span class="sxs-lookup"><span data-stu-id="cb414-132">If you choose a cluster that hasn't been enabled to work with Azure Dev Spaces, you'll see a message asking if you want to configure it.</span></span>

![](media/get-started-netcore-visualstudio/Add-Azure-Dev-Spaces-Resource.png)

<span data-ttu-id="cb414-133">Choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb414-133">Choose **OK**.</span></span>

 <span data-ttu-id="cb414-134">A background task will be started to accomplish this.</span><span class="sxs-lookup"><span data-stu-id="cb414-134">A background task will be started to accomplish this.</span></span> <span data-ttu-id="cb414-135">It will take a number of minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="cb414-135">It will take a number of minutes to complete.</span></span> <span data-ttu-id="cb414-136">To see if it's still being created, hover your pointer over the **Background tasks** icon in the bottom left corner of the status bar, as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="cb414-136">To see if it's still being created, hover your pointer over the **Background tasks** icon in the bottom left corner of the status bar, as shown in the following image.</span></span>

![](media/get-started-netcore-visualstudio/BackgroundTasks.PNG)

> [!Note]
> <span data-ttu-id="cb414-137">Until the dev space is successfully created you cannot debug your application.</span><span class="sxs-lookup"><span data-stu-id="cb414-137">Until the dev space is successfully created you cannot debug your application.</span></span>

### <a name="look-at-the-files-added-to-project"></a><span data-ttu-id="cb414-138">Look at the files added to project</span><span class="sxs-lookup"><span data-stu-id="cb414-138">Look at the files added to project</span></span>
<span data-ttu-id="cb414-139">While you wait for the dev space to be created, look at the files that have been added to your project when you chose to use a dev space.</span><span class="sxs-lookup"><span data-stu-id="cb414-139">While you wait for the dev space to be created, look at the files that have been added to your project when you chose to use a dev space.</span></span>

<span data-ttu-id="cb414-140">First, you can see a folder named `charts` has been added and within this folder a [Helm chart](https://docs.helm.sh) for your application has been scaffolded.</span><span class="sxs-lookup"><span data-stu-id="cb414-140">First, you can see a folder named `charts` has been added and within this folder a [Helm chart](https://docs.helm.sh) for your application has been scaffolded.</span></span> <span data-ttu-id="cb414-141">These files are used to deploy your application into the dev space.</span><span class="sxs-lookup"><span data-stu-id="cb414-141">These files are used to deploy your application into the dev space.</span></span>

<span data-ttu-id="cb414-142">You will see a file named `Dockerfile` has been added.</span><span class="sxs-lookup"><span data-stu-id="cb414-142">You will see a file named `Dockerfile` has been added.</span></span> <span data-ttu-id="cb414-143">This file has information needed to package your application in the standard Docker format.</span><span class="sxs-lookup"><span data-stu-id="cb414-143">This file has information needed to package your application in the standard Docker format.</span></span>

<span data-ttu-id="cb414-144">Lastly, you will see a file named `azds.yaml`, which contains development-time configuration that is needed by the dev space.</span><span class="sxs-lookup"><span data-stu-id="cb414-144">Lastly, you will see a file named `azds.yaml`, which contains development-time configuration that is needed by the dev space.</span></span>

![](media/get-started-netcore-visualstudio/ProjectFiles.png)

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="cb414-145">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cb414-145">Debug a container in Kubernetes</span></span>
<span data-ttu-id="cb414-146">Once the dev space is successfully created, you can debug the application.</span><span class="sxs-lookup"><span data-stu-id="cb414-146">Once the dev space is successfully created, you can debug the application.</span></span> <span data-ttu-id="cb414-147">Set a breakpoint in the code, for example on line 20 in the file `HomeController.cs` where the `Message` variable is set.</span><span class="sxs-lookup"><span data-stu-id="cb414-147">Set a breakpoint in the code, for example on line 20 in the file `HomeController.cs` where the `Message` variable is set.</span></span> <span data-ttu-id="cb414-148">Click **F5** to start debugging.</span><span class="sxs-lookup"><span data-stu-id="cb414-148">Click **F5** to start debugging.</span></span> 

<span data-ttu-id="cb414-149">Visual Studio will communicate with the dev space to build and deploy the application and then open a browser with the web app running.</span><span class="sxs-lookup"><span data-stu-id="cb414-149">Visual Studio will communicate with the dev space to build and deploy the application and then open a browser with the web app running.</span></span> <span data-ttu-id="cb414-150">It might seem like the container is running locally, but actually it's running in the dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb414-150">It might seem like the container is running locally, but actually it's running in the dev space in Azure.</span></span> <span data-ttu-id="cb414-151">The reason for the localhost address is because Azure Dev Spaces creates a temporary SSH tunnel to the container running in AKS.</span><span class="sxs-lookup"><span data-stu-id="cb414-151">The reason for the localhost address is because Azure Dev Spaces creates a temporary SSH tunnel to the container running in AKS.</span></span>

<span data-ttu-id="cb414-152">Click on the **About** link at the top of the page to trigger the breakpoint.</span><span class="sxs-lookup"><span data-stu-id="cb414-152">Click on the **About** link at the top of the page to trigger the breakpoint.</span></span> <span data-ttu-id="cb414-153">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, and so on.</span><span class="sxs-lookup"><span data-stu-id="cb414-153">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, and so on.</span></span>

## <a name="iteratively-develop-code"></a><span data-ttu-id="cb414-154">Iteratively develop code</span><span class="sxs-lookup"><span data-stu-id="cb414-154">Iteratively develop code</span></span>

<span data-ttu-id="cb414-155">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="cb414-155">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span></span>

### <a name="update-a-content-file"></a><span data-ttu-id="cb414-156">Update a content file</span><span class="sxs-lookup"><span data-stu-id="cb414-156">Update a content file</span></span>
1. <span data-ttu-id="cb414-157">Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML.</span><span class="sxs-lookup"><span data-stu-id="cb414-157">Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML.</span></span> <span data-ttu-id="cb414-158">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span><span class="sxs-lookup"><span data-stu-id="cb414-158">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span></span>
1. <span data-ttu-id="cb414-159">Save the file.</span><span class="sxs-lookup"><span data-stu-id="cb414-159">Save the file.</span></span>
1. <span data-ttu-id="cb414-160">Go to your browser and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="cb414-160">Go to your browser and refresh the page.</span></span> <span data-ttu-id="cb414-161">You should see the web page display the updated HTML.</span><span class="sxs-lookup"><span data-stu-id="cb414-161">You should see the web page display the updated HTML.</span></span>

<span data-ttu-id="cb414-162">What happened?</span><span class="sxs-lookup"><span data-stu-id="cb414-162">What happened?</span></span> <span data-ttu-id="cb414-163">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active F5 session automatically syncs any modified content files into the running container in AKS, so you can see your content edits right away.</span><span class="sxs-lookup"><span data-stu-id="cb414-163">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active F5 session automatically syncs any modified content files into the running container in AKS, so you can see your content edits right away.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="cb414-164">Update a code file</span><span class="sxs-lookup"><span data-stu-id="cb414-164">Update a code file</span></span>
<span data-ttu-id="cb414-165">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span><span class="sxs-lookup"><span data-stu-id="cb414-165">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span></span>

1. <span data-ttu-id="cb414-166">Stop the debugger in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb414-166">Stop the debugger in Visual Studio.</span></span>
1. <span data-ttu-id="cb414-167">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span><span class="sxs-lookup"><span data-stu-id="cb414-167">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span></span>
1. <span data-ttu-id="cb414-168">Save the file.</span><span class="sxs-lookup"><span data-stu-id="cb414-168">Save the file.</span></span>
1. <span data-ttu-id="cb414-169">Press **F5** to start debugging again.</span><span class="sxs-lookup"><span data-stu-id="cb414-169">Press **F5** to start debugging again.</span></span> 

<span data-ttu-id="cb414-170">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="cb414-170">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="cb414-171">Refresh the web app in the browser, and go to the About page.</span><span class="sxs-lookup"><span data-stu-id="cb414-171">Refresh the web app in the browser, and go to the About page.</span></span> <span data-ttu-id="cb414-172">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="cb414-172">You should see your custom message appear in the UI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb414-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb414-173">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb414-174">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="cb414-174">Learn about team development</span></span>](team-development-netcore-visualstudio.md)
