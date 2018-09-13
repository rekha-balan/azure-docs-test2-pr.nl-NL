---
title: Create a Kubernetes dev space in the cloud | Microsoft Docs
titleSuffix: Azure Dev Spaces
author: ghogen
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
ms.author: ghogen
ms.date: 07/09/2018
ms.topic: quickstart
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: douge
ms.openlocfilehash: 600625f143041eaf983b7ec7e945c5a968b522f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855671"
---
# <a name="quickstart-create-a-kubernetes-dev-space-with-azure-dev-spaces-net-core-and-visual-studio"></a><span data-ttu-id="cb5d5-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (.NET Core and Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="cb5d5-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (.NET Core and Visual Studio)</span></span>

<span data-ttu-id="cb5d5-105">In this guide, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="cb5d5-105">In this guide, you will learn how to:</span></span>

- <span data-ttu-id="cb5d5-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span></span>
- <span data-ttu-id="cb5d5-107">Iteratively develop code in containers using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-107">Iteratively develop code in containers using Visual Studio.</span></span>
- <span data-ttu-id="cb5d5-108">Debug code running in your cluster.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-108">Debug code running in your cluster.</span></span>

> [!Note]
> <span data-ttu-id="cb5d5-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span></span> <span data-ttu-id="cb5d5-110">You can also try the more detailed [tutorial](get-started-netcore-visualstudio.md).</span><span class="sxs-lookup"><span data-stu-id="cb5d5-110">You can also try the more detailed [tutorial](get-started-netcore-visualstudio.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb5d5-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cb5d5-111">Prerequisites</span></span>

- <span data-ttu-id="cb5d5-112">A Kubernetes cluster running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with Http Application Routing enabled.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-112">A Kubernetes cluster running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with Http Application Routing enabled.</span></span>

  ![Be sure to enable Http Application Routing.](media/common/Kubernetes-Create-Cluster-3.PNG)

- <span data-ttu-id="cb5d5-114">Visual Studio 2017 with the Web Development workload installed.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-114">Visual Studio 2017 with the Web Development workload installed.</span></span> <span data-ttu-id="cb5d5-115">If you don't have it installed, download it [here](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span><span class="sxs-lookup"><span data-stu-id="cb5d5-115">If you don't have it installed, download it [here](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs).</span></span>

## <a name="set-up-azure-dev-spaces"></a><span data-ttu-id="cb5d5-116">Set up Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="cb5d5-116">Set up Azure Dev Spaces</span></span>

<span data-ttu-id="cb5d5-117">Install [Visual Studio Tools for Kubernetes](https://aka.ms/get-azds-visualstudio).</span><span class="sxs-lookup"><span data-stu-id="cb5d5-117">Install [Visual Studio Tools for Kubernetes](https://aka.ms/get-azds-visualstudio).</span></span>

## <a name="connect-to-a-cluster"></a><span data-ttu-id="cb5d5-118">Connect to a cluster</span><span class="sxs-lookup"><span data-stu-id="cb5d5-118">Connect to a cluster</span></span>

<span data-ttu-id="cb5d5-119">Next, you'll create and configure a project for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-119">Next, you'll create and configure a project for Azure Dev Spaces.</span></span>

### <a name="create-an-aspnet-web-app"></a><span data-ttu-id="cb5d5-120">Create an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="cb5d5-120">Create an ASP.NET web app</span></span>

<span data-ttu-id="cb5d5-121">From within Visual Studio 2017, create a new project.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-121">From within Visual Studio 2017, create a new project.</span></span> <span data-ttu-id="cb5d5-122">Currently, the project must be an **ASP.NET Core Web Application**.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-122">Currently, the project must be an **ASP.NET Core Web Application**.</span></span> <span data-ttu-id="cb5d5-123">Name the project **webfrontend**.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-123">Name the project **webfrontend**.</span></span>

<span data-ttu-id="cb5d5-124">Select the **Web Application (Model-View-Controller)** template and be sure you're targeting **.NET Core** and **ASP.NET Core 2.0**.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-124">Select the **Web Application (Model-View-Controller)** template and be sure you're targeting **.NET Core** and **ASP.NET Core 2.0**.</span></span>

### <a name="enable-dev-spaces-for-an-aks-cluster"></a><span data-ttu-id="cb5d5-125">Enable Dev Spaces for an AKS cluster</span><span class="sxs-lookup"><span data-stu-id="cb5d5-125">Enable Dev Spaces for an AKS cluster</span></span>

<span data-ttu-id="cb5d5-126">With the project you just created, select **Azure Dev Spaces** from the launch settings dropdown, as shown below.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-126">With the project you just created, select **Azure Dev Spaces** from the launch settings dropdown, as shown below.</span></span>

![](media/get-started-netcore-visualstudio/LaunchSettings.png)

<span data-ttu-id="cb5d5-127">In the dialog that is displayed next, make sure you are signed in with the appropriate account, and then select an existing cluster.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-127">In the dialog that is displayed next, make sure you are signed in with the appropriate account, and then select an existing cluster.</span></span>

![](media/get-started-netcore-visualstudio/Azure-Dev-Spaces-Dialog.png)

<span data-ttu-id="cb5d5-128">Leave the **Space** dropdown set to `default` for now.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-128">Leave the **Space** dropdown set to `default` for now.</span></span> <span data-ttu-id="cb5d5-129">Check the **Publicly Accessible** checkbox so the web app will be accessible via a public endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-129">Check the **Publicly Accessible** checkbox so the web app will be accessible via a public endpoint.</span></span>

![](media/get-started-netcore-visualstudio/Azure-Dev-Spaces-Dialog2.png)

<span data-ttu-id="cb5d5-130">Click **OK** to select or create the cluster.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-130">Click **OK** to select or create the cluster.</span></span>

<span data-ttu-id="cb5d5-131">If you choose a cluster that hasn't been configured to work with Azure Dev Spaces, you'll see a message asking if you want to configure it.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-131">If you choose a cluster that hasn't been configured to work with Azure Dev Spaces, you'll see a message asking if you want to configure it.</span></span>

![](media/get-started-netcore-visualstudio/Add-Azure-Dev-Spaces-Resource.png)

<span data-ttu-id="cb5d5-132">Choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-132">Choose **OK**.</span></span> 

### <a name="look-at-the-files-added-to-project"></a><span data-ttu-id="cb5d5-133">Look at the files added to project</span><span class="sxs-lookup"><span data-stu-id="cb5d5-133">Look at the files added to project</span></span>
<span data-ttu-id="cb5d5-134">While you wait for the dev space to be created, look at the files that have been added to your project when you chose to use Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-134">While you wait for the dev space to be created, look at the files that have been added to your project when you chose to use Azure Dev Spaces.</span></span>

- <span data-ttu-id="cb5d5-135">A folder named `charts` has been added and within this folder a [Helm chart](https://docs.helm.sh) for your application has been scaffolded.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-135">A folder named `charts` has been added and within this folder a [Helm chart](https://docs.helm.sh) for your application has been scaffolded.</span></span> <span data-ttu-id="cb5d5-136">These files are used to deploy your application into the dev space.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-136">These files are used to deploy your application into the dev space.</span></span>
- <span data-ttu-id="cb5d5-137">`Dockerfile` has information needed to package your application in the standard Docker format.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-137">`Dockerfile` has information needed to package your application in the standard Docker format.</span></span>
- <span data-ttu-id="cb5d5-138">`azds.yaml` contains development-time configuration that is needed by the dev space.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-138">`azds.yaml` contains development-time configuration that is needed by the dev space.</span></span>

![](media/get-started-netcore-visualstudio/ProjectFiles.png)

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="cb5d5-139">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cb5d5-139">Debug a container in Kubernetes</span></span>
<span data-ttu-id="cb5d5-140">Once the dev space is successfully created, you can debug the application.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-140">Once the dev space is successfully created, you can debug the application.</span></span> <span data-ttu-id="cb5d5-141">Set a breakpoint in the code, for example on line 20 in the file `HomeController.cs` where the `Message` variable is set.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-141">Set a breakpoint in the code, for example on line 20 in the file `HomeController.cs` where the `Message` variable is set.</span></span> <span data-ttu-id="cb5d5-142">Click **F5** to start debugging.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-142">Click **F5** to start debugging.</span></span> 

<span data-ttu-id="cb5d5-143">Visual Studio will communicate with the dev space to build and deploy the application and then open a browser with the web app running.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-143">Visual Studio will communicate with the dev space to build and deploy the application and then open a browser with the web app running.</span></span> <span data-ttu-id="cb5d5-144">It might seem like the container is running locally, but actually it's running in the dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-144">It might seem like the container is running locally, but actually it's running in the dev space in Azure.</span></span> <span data-ttu-id="cb5d5-145">The reason for the localhost address is because Azure Dev Spaces creates a temporary SSH tunnel to the container running in AKS.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-145">The reason for the localhost address is because Azure Dev Spaces creates a temporary SSH tunnel to the container running in AKS.</span></span>

<span data-ttu-id="cb5d5-146">Click on the **About** link at the top of the page to trigger the breakpoint.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-146">Click on the **About** link at the top of the page to trigger the breakpoint.</span></span> <span data-ttu-id="cb5d5-147">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, and so on.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-147">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, and so on.</span></span>


## <a name="iteratively-develop-code"></a><span data-ttu-id="cb5d5-148">Iteratively develop code</span><span class="sxs-lookup"><span data-stu-id="cb5d5-148">Iteratively develop code</span></span>

<span data-ttu-id="cb5d5-149">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-149">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span></span>

### <a name="update-a-content-file"></a><span data-ttu-id="cb5d5-150">Update a content file</span><span class="sxs-lookup"><span data-stu-id="cb5d5-150">Update a content file</span></span>
1. <span data-ttu-id="cb5d5-151">Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-151">Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML.</span></span> <span data-ttu-id="cb5d5-152">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span><span class="sxs-lookup"><span data-stu-id="cb5d5-152">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span></span>
1. <span data-ttu-id="cb5d5-153">Save the file.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-153">Save the file.</span></span>
1. <span data-ttu-id="cb5d5-154">Go to your browser and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-154">Go to your browser and refresh the page.</span></span> <span data-ttu-id="cb5d5-155">You should see the web page display the updated HTML.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-155">You should see the web page display the updated HTML.</span></span>

<span data-ttu-id="cb5d5-156">What happened?</span><span class="sxs-lookup"><span data-stu-id="cb5d5-156">What happened?</span></span> <span data-ttu-id="cb5d5-157">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active F5 session automatically syncs any modified content files into the running container in AKS, so you can see your content edits right away.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-157">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active F5 session automatically syncs any modified content files into the running container in AKS, so you can see your content edits right away.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="cb5d5-158">Update a code file</span><span class="sxs-lookup"><span data-stu-id="cb5d5-158">Update a code file</span></span>
<span data-ttu-id="cb5d5-159">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-159">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span></span>

1. <span data-ttu-id="cb5d5-160">Stop the debugger in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-160">Stop the debugger in Visual Studio.</span></span>
1. <span data-ttu-id="cb5d5-161">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span><span class="sxs-lookup"><span data-stu-id="cb5d5-161">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span></span>
1. <span data-ttu-id="cb5d5-162">Save the file.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-162">Save the file.</span></span>
1. <span data-ttu-id="cb5d5-163">Press **F5** to start debugging again.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-163">Press **F5** to start debugging again.</span></span> 

<span data-ttu-id="cb5d5-164">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-164">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="cb5d5-165">Refresh the web app in the browser, and go to the About page.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-165">Refresh the web app in the browser, and go to the About page.</span></span> <span data-ttu-id="cb5d5-166">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="cb5d5-166">You should see your custom message appear in the UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb5d5-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="cb5d5-167">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb5d5-168">Working with multiple containers and team development</span><span class="sxs-lookup"><span data-stu-id="cb5d5-168">Working with multiple containers and team development</span></span>](team-development-netcore-visualstudio.md)
