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
ms.openlocfilehash: 1fa3ddd605ba410093542795c1c805906f98a1f5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965853"
---
# <a name="quickstart-create-a-kubernetes-dev-space-with-azure-dev-spaces-net-core-and-vs-code"></a><span data-ttu-id="bc147-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (.NET Core and VS Code)</span><span class="sxs-lookup"><span data-stu-id="bc147-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (.NET Core and VS Code)</span></span>

<span data-ttu-id="bc147-105">In this guide, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="bc147-105">In this guide, you will learn how to:</span></span>

- <span data-ttu-id="bc147-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc147-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span></span>
- <span data-ttu-id="bc147-107">Iteratively develop code in containers using VS Code and the command line.</span><span class="sxs-lookup"><span data-stu-id="bc147-107">Iteratively develop code in containers using VS Code and the command line.</span></span>
- <span data-ttu-id="bc147-108">Debug the code in your dev space from VS Code</span><span class="sxs-lookup"><span data-stu-id="bc147-108">Debug the code in your dev space from VS Code</span></span>

> [!Note]
> <span data-ttu-id="bc147-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span><span class="sxs-lookup"><span data-stu-id="bc147-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span></span> <span data-ttu-id="bc147-110">You can also try the more detailed [tutorial](get-started-netcore.md).</span><span class="sxs-lookup"><span data-stu-id="bc147-110">You can also try the more detailed [tutorial](get-started-netcore.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc147-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc147-111">Prerequisites</span></span>

- <span data-ttu-id="bc147-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bc147-112">An Azure subscription.</span></span> <span data-ttu-id="bc147-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="bc147-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/free).</span></span>
- <span data-ttu-id="bc147-114">A [Kubernetes cluster](https://ms.portal.azure.com/#create/microsoft.aks) running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with **Http Application Routing** enabled.</span><span class="sxs-lookup"><span data-stu-id="bc147-114">A [Kubernetes cluster](https://ms.portal.azure.com/#create/microsoft.aks) running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with **Http Application Routing** enabled.</span></span>

  ![Be sure to enable Http Application Routing.](media/common/Kubernetes-Create-Cluster-3.PNG)

- <span data-ttu-id="bc147-116">[Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="bc147-116">[Visual Studio Code](https://code.visualstudio.com/download).</span></span>

## <a name="set-up-azure-dev-spaces"></a><span data-ttu-id="bc147-117">Set up Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="bc147-117">Set up Azure Dev Spaces</span></span>

<span data-ttu-id="bc147-118">The Azure CLI and the Azure Dev Spaces extension can be installed and run on Windows, Mac, or Linux machines.</span><span class="sxs-lookup"><span data-stu-id="bc147-118">The Azure CLI and the Azure Dev Spaces extension can be installed and run on Windows, Mac, or Linux machines.</span></span> <span data-ttu-id="bc147-119">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span><span class="sxs-lookup"><span data-stu-id="bc147-119">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span></span>

<span data-ttu-id="bc147-120">Follow these steps to set up Azure Dev Spaces:</span><span class="sxs-lookup"><span data-stu-id="bc147-120">Follow these steps to set up Azure Dev Spaces:</span></span>

1. <span data-ttu-id="bc147-121">Install the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) (version 2.0.43 or higher).</span><span class="sxs-lookup"><span data-stu-id="bc147-121">Install the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) (version 2.0.43 or higher).</span></span>
1. <span data-ttu-id="bc147-122">Set up Dev Spaces on your AKS cluster: `az aks use-dev-spaces -g MyResourceGroup -n MyAKS`</span><span class="sxs-lookup"><span data-stu-id="bc147-122">Set up Dev Spaces on your AKS cluster: `az aks use-dev-spaces -g MyResourceGroup -n MyAKS`</span></span>
1. <span data-ttu-id="bc147-123">Download the [Azure Dev Spaces extension](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds) for VS Code.</span><span class="sxs-lookup"><span data-stu-id="bc147-123">Download the [Azure Dev Spaces extension](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds) for VS Code.</span></span> <span data-ttu-id="bc147-124">Click Install once on the extension's Marketplace page, and again in VS Code.</span><span class="sxs-lookup"><span data-stu-id="bc147-124">Click Install once on the extension's Marketplace page, and again in VS Code.</span></span>

## <a name="build-and-run-code-in-kubernetes"></a><span data-ttu-id="bc147-125">Build and run code in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bc147-125">Build and run code in Kubernetes</span></span>

1. <span data-ttu-id="bc147-126">Download sample code from GitHub: [https://github.com/Azure/dev-spaces](https://github.com/Azure/dev-spaces)</span><span class="sxs-lookup"><span data-stu-id="bc147-126">Download sample code from GitHub: [https://github.com/Azure/dev-spaces](https://github.com/Azure/dev-spaces)</span></span> 
1. <span data-ttu-id="bc147-127">Change directory to the webfrontend folder: `cd dev-spaces/samples/dotnetcore/getting-started/webfrontend`</span><span class="sxs-lookup"><span data-stu-id="bc147-127">Change directory to the webfrontend folder: `cd dev-spaces/samples/dotnetcore/getting-started/webfrontend`</span></span>
1. <span data-ttu-id="bc147-128">Generate Docker and Helm chart assets: `azds prep --public`</span><span class="sxs-lookup"><span data-stu-id="bc147-128">Generate Docker and Helm chart assets: `azds prep --public`</span></span>
1. <span data-ttu-id="bc147-129">Build and run your code in AKS.</span><span class="sxs-lookup"><span data-stu-id="bc147-129">Build and run your code in AKS.</span></span> <span data-ttu-id="bc147-130">In the terminal window from the **webfrontend folder**, run this command: `azds up`</span><span class="sxs-lookup"><span data-stu-id="bc147-130">In the terminal window from the **webfrontend folder**, run this command: `azds up`</span></span>
1. <span data-ttu-id="bc147-131">Scan the console output for information about the URL that was created by the `up` command.</span><span class="sxs-lookup"><span data-stu-id="bc147-131">Scan the console output for information about the URL that was created by the `up` command.</span></span> <span data-ttu-id="bc147-132">It will be in the form:</span><span class="sxs-lookup"><span data-stu-id="bc147-132">It will be in the form:</span></span> 

   `Service 'webfrontend' port 'http' is available at <url>` 

   <span data-ttu-id="bc147-133">Open this URL in a browser window, and you should see the web app load.</span><span class="sxs-lookup"><span data-stu-id="bc147-133">Open this URL in a browser window, and you should see the web app load.</span></span> 
   
   > [!Note]
   > <span data-ttu-id="bc147-134">On first run, it can take several minutes for public DNS to be ready.</span><span class="sxs-lookup"><span data-stu-id="bc147-134">On first run, it can take several minutes for public DNS to be ready.</span></span> <span data-ttu-id="bc147-135">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span><span class="sxs-lookup"><span data-stu-id="bc147-135">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span></span> <span data-ttu-id="bc147-136">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span><span class="sxs-lookup"><span data-stu-id="bc147-136">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span></span> <span data-ttu-id="bc147-137">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc147-137">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span> <span data-ttu-id="bc147-138">You can come back and try the public URL later when the DNS record is ready.</span><span class="sxs-lookup"><span data-stu-id="bc147-138">You can come back and try the public URL later when the DNS record is ready.</span></span>

### <a name="update-a-content-file"></a><span data-ttu-id="bc147-139">Update a content file</span><span class="sxs-lookup"><span data-stu-id="bc147-139">Update a content file</span></span>

1. <span data-ttu-id="bc147-140">Locate a file, such as `./Views/Home/Index.cshtml`, and make an edit to the HTML.</span><span class="sxs-lookup"><span data-stu-id="bc147-140">Locate a file, such as `./Views/Home/Index.cshtml`, and make an edit to the HTML.</span></span> <span data-ttu-id="bc147-141">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span><span class="sxs-lookup"><span data-stu-id="bc147-141">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span></span>
1. <span data-ttu-id="bc147-142">Save the file.</span><span class="sxs-lookup"><span data-stu-id="bc147-142">Save the file.</span></span> <span data-ttu-id="bc147-143">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span><span class="sxs-lookup"><span data-stu-id="bc147-143">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span></span>
1. <span data-ttu-id="bc147-144">Go to your browser and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="bc147-144">Go to your browser and refresh the page.</span></span> <span data-ttu-id="bc147-145">You should see the web page display the updated HTML.</span><span class="sxs-lookup"><span data-stu-id="bc147-145">You should see the web page display the updated HTML.</span></span>

<span data-ttu-id="bc147-146">What happened?</span><span class="sxs-lookup"><span data-stu-id="bc147-146">What happened?</span></span> <span data-ttu-id="bc147-147">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active `azds up` command automatically syncs any modified content files into the running container in Azure, so you can see your content edits right away.</span><span class="sxs-lookup"><span data-stu-id="bc147-147">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active `azds up` command automatically syncs any modified content files into the running container in Azure, so you can see your content edits right away.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="bc147-148">Update a code file</span><span class="sxs-lookup"><span data-stu-id="bc147-148">Update a code file</span></span>
<span data-ttu-id="bc147-149">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span><span class="sxs-lookup"><span data-stu-id="bc147-149">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span></span>

1. <span data-ttu-id="bc147-150">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span><span class="sxs-lookup"><span data-stu-id="bc147-150">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span></span>
1. <span data-ttu-id="bc147-151">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span><span class="sxs-lookup"><span data-stu-id="bc147-151">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span></span>
1. <span data-ttu-id="bc147-152">Save the file.</span><span class="sxs-lookup"><span data-stu-id="bc147-152">Save the file.</span></span>
1. <span data-ttu-id="bc147-153">Run  `azds up` in the terminal window.</span><span class="sxs-lookup"><span data-stu-id="bc147-153">Run  `azds up` in the terminal window.</span></span> 

<span data-ttu-id="bc147-154">This command rebuilds the container image and redeploys the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="bc147-154">This command rebuilds the container image and redeploys the Helm chart.</span></span> <span data-ttu-id="bc147-155">To see your code changes take effect in the running application, go to the About menu in the web app.</span><span class="sxs-lookup"><span data-stu-id="bc147-155">To see your code changes take effect in the running application, go to the About menu in the web app.</span></span>

<span data-ttu-id="bc147-156">But there is an even *faster method* for developing code, which you'll explore in the next section.</span><span class="sxs-lookup"><span data-stu-id="bc147-156">But there is an even *faster method* for developing code, which you'll explore in the next section.</span></span> 

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="bc147-157">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bc147-157">Debug a container in Kubernetes</span></span>

<span data-ttu-id="bc147-158">In this section, you'll use VS Code to directly debug your container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc147-158">In this section, you'll use VS Code to directly debug your container running in Azure.</span></span> <span data-ttu-id="bc147-159">You'll also learn how to get a faster edit-run-test loop.</span><span class="sxs-lookup"><span data-stu-id="bc147-159">You'll also learn how to get a faster edit-run-test loop.</span></span>

![](./media/common/edit-refresh-see.png)

### <a name="initialize-debug-assets-with-the-vs-code-extension"></a><span data-ttu-id="bc147-160">Initialize debug assets with the VS Code extension</span><span class="sxs-lookup"><span data-stu-id="bc147-160">Initialize debug assets with the VS Code extension</span></span>
<span data-ttu-id="bc147-161">You first need to configure your code project so VS Code will communicate with the dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="bc147-161">You first need to configure your code project so VS Code will communicate with the dev space in Azure.</span></span> <span data-ttu-id="bc147-162">The VS Code extension for Azure Dev Spaces provides a helper command to set up debug configuration.</span><span class="sxs-lookup"><span data-stu-id="bc147-162">The VS Code extension for Azure Dev Spaces provides a helper command to set up debug configuration.</span></span> 

<span data-ttu-id="bc147-163">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span><span class="sxs-lookup"><span data-stu-id="bc147-163">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span></span> 

<span data-ttu-id="bc147-164">This adds debug configuration for Azure Dev Spaces under the `.vscode` folder.</span><span class="sxs-lookup"><span data-stu-id="bc147-164">This adds debug configuration for Azure Dev Spaces under the `.vscode` folder.</span></span> <span data-ttu-id="bc147-165">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span><span class="sxs-lookup"><span data-stu-id="bc147-165">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span></span>

![](./media/common/command-palette.png)

### <a name="select-the-azds-debug-configuration"></a><span data-ttu-id="bc147-166">Select the AZDS debug configuration</span><span class="sxs-lookup"><span data-stu-id="bc147-166">Select the AZDS debug configuration</span></span>
1. <span data-ttu-id="bc147-167">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="bc147-167">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span>
1. <span data-ttu-id="bc147-168">Select **.NET Core Launch (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="bc147-168">Select **.NET Core Launch (AZDS)** as the active debug configuration.</span></span>

![](media/get-started-netcore/debug-configuration.png)

> [!Note]
> <span data-ttu-id="bc147-169">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="bc147-169">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span></span> <span data-ttu-id="bc147-170">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span><span class="sxs-lookup"><span data-stu-id="bc147-170">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span></span>


### <a name="debug-the-container-in-kubernetes"></a><span data-ttu-id="bc147-171">Debug the container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bc147-171">Debug the container in Kubernetes</span></span>
<span data-ttu-id="bc147-172">Hit **F5** to debug your code in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bc147-172">Hit **F5** to debug your code in Kubernetes.</span></span>

<span data-ttu-id="bc147-173">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bc147-173">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span></span> <span data-ttu-id="bc147-174">This time, of course, the debugger is attached to the remote container.</span><span class="sxs-lookup"><span data-stu-id="bc147-174">This time, of course, the debugger is attached to the remote container.</span></span>

> [!Tip]
> <span data-ttu-id="bc147-175">The VS Code status bar will display a clickable URL.</span><span class="sxs-lookup"><span data-stu-id="bc147-175">The VS Code status bar will display a clickable URL.</span></span>

<span data-ttu-id="bc147-176">Set a breakpoint in a server-side code file, for example within the `Index()` function in the `Controllers/HomeController.cs` source file.</span><span class="sxs-lookup"><span data-stu-id="bc147-176">Set a breakpoint in a server-side code file, for example within the `Index()` function in the `Controllers/HomeController.cs` source file.</span></span> <span data-ttu-id="bc147-177">Refreshing the browser page causes the breakpoint to be hit.</span><span class="sxs-lookup"><span data-stu-id="bc147-177">Refreshing the browser page causes the breakpoint to be hit.</span></span>

<span data-ttu-id="bc147-178">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span><span class="sxs-lookup"><span data-stu-id="bc147-178">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span></span>

### <a name="edit-code-and-refresh"></a><span data-ttu-id="bc147-179">Edit code and refresh</span><span class="sxs-lookup"><span data-stu-id="bc147-179">Edit code and refresh</span></span>
<span data-ttu-id="bc147-180">With the debugger active, make a code edit.</span><span class="sxs-lookup"><span data-stu-id="bc147-180">With the debugger active, make a code edit.</span></span> <span data-ttu-id="bc147-181">For example, modify the About page's message in `Controllers/HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="bc147-181">For example, modify the About page's message in `Controllers/HomeController.cs`.</span></span> 

```csharp
public IActionResult About()
{
    ViewData["Message"] = "My custom message in the About page.";
    return View();
}
```

<span data-ttu-id="bc147-182">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="bc147-182">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span></span> 

![](media/get-started-netcore/debug-action-refresh.png)

<span data-ttu-id="bc147-183">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="bc147-183">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="bc147-184">Refresh the web app in the browser, and go to the About page.</span><span class="sxs-lookup"><span data-stu-id="bc147-184">Refresh the web app in the browser, and go to the About page.</span></span> <span data-ttu-id="bc147-185">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="bc147-185">You should see your custom message appear in the UI.</span></span>

<span data-ttu-id="bc147-186">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span><span class="sxs-lookup"><span data-stu-id="bc147-186">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc147-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc147-187">Next steps</span></span>

<span data-ttu-id="bc147-188">Learn how Azure Dev Spaces helps you develop more complex apps across multiple containers, and how you can simplify collaborative development by working with different versions or branches of your code in different spaces.</span><span class="sxs-lookup"><span data-stu-id="bc147-188">Learn how Azure Dev Spaces helps you develop more complex apps across multiple containers, and how you can simplify collaborative development by working with different versions or branches of your code in different spaces.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc147-189">Working with multiple containers and team development</span><span class="sxs-lookup"><span data-stu-id="bc147-189">Working with multiple containers and team development</span></span>](team-development-netcore.md)
