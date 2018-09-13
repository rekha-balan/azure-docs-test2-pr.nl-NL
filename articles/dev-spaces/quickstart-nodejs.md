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
ms.openlocfilehash: 671cf3d274f067354131777b9f69d75c6a9fc934
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869747"
---
# <a name="quickstart-create-a-kubernetes-dev-space-with-azure-dev-spaces-nodejs"></a><span data-ttu-id="216c9-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (Node.js)</span><span class="sxs-lookup"><span data-stu-id="216c9-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (Node.js)</span></span>

<span data-ttu-id="216c9-105">In this guide, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="216c9-105">In this guide, you will learn how to:</span></span>

- <span data-ttu-id="216c9-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="216c9-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span></span>
- <span data-ttu-id="216c9-107">Iteratively develop code in containers using VS Code and the command line.</span><span class="sxs-lookup"><span data-stu-id="216c9-107">Iteratively develop code in containers using VS Code and the command line.</span></span>
- <span data-ttu-id="216c9-108">Debug code running in your cluster.</span><span class="sxs-lookup"><span data-stu-id="216c9-108">Debug code running in your cluster.</span></span>

> [!Note]
> <span data-ttu-id="216c9-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span><span class="sxs-lookup"><span data-stu-id="216c9-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span></span> <span data-ttu-id="216c9-110">You can also try the more detailed [tutorial](get-started-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="216c9-110">You can also try the more detailed [tutorial](get-started-nodejs.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="216c9-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="216c9-111">Prerequisites</span></span>

- <span data-ttu-id="216c9-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="216c9-112">An Azure subscription.</span></span> <span data-ttu-id="216c9-113">If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="216c9-113">If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free).</span></span>
- <span data-ttu-id="216c9-114">A [Kubernetes cluster](https://ms.portal.azure.com/#create/microsoft.aks) running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with **Http Application Routing** enabled.</span><span class="sxs-lookup"><span data-stu-id="216c9-114">A [Kubernetes cluster](https://ms.portal.azure.com/#create/microsoft.aks) running Kubernetes 1.9.6 or later, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with **Http Application Routing** enabled.</span></span>

  ![Be sure to enable Http Application Routing.](media/common/Kubernetes-Create-Cluster-3.PNG)

- <span data-ttu-id="216c9-116">Visual Studio Code, which you can download [here](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="216c9-116">Visual Studio Code, which you can download [here](https://code.visualstudio.com/download).</span></span>

## <a name="set-up-azure-dev-spaces"></a><span data-ttu-id="216c9-117">Set up Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="216c9-117">Set up Azure Dev Spaces</span></span>

<span data-ttu-id="216c9-118">The Azure CLI and the Azure Dev Spaces extension can be installed and run on Windows, Mac, or Linux machines.</span><span class="sxs-lookup"><span data-stu-id="216c9-118">The Azure CLI and the Azure Dev Spaces extension can be installed and run on Windows, Mac, or Linux machines.</span></span> <span data-ttu-id="216c9-119">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span><span class="sxs-lookup"><span data-stu-id="216c9-119">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span></span>

<span data-ttu-id="216c9-120">Follow these steps to set up Azure Dev Spaces:</span><span class="sxs-lookup"><span data-stu-id="216c9-120">Follow these steps to set up Azure Dev Spaces:</span></span>

1. <span data-ttu-id="216c9-121">Install the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) (version 2.0.43 or higher).</span><span class="sxs-lookup"><span data-stu-id="216c9-121">Install the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) (version 2.0.43 or higher).</span></span>
1. <span data-ttu-id="216c9-122">Set up Dev Spaces on your AKS cluster: `az aks use-dev-spaces -g MyResourceGroup -n MyAKS`</span><span class="sxs-lookup"><span data-stu-id="216c9-122">Set up Dev Spaces on your AKS cluster: `az aks use-dev-spaces -g MyResourceGroup -n MyAKS`</span></span>
1. <span data-ttu-id="216c9-123">Download the [Azure Dev Spaces extension](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds) for VS Code.</span><span class="sxs-lookup"><span data-stu-id="216c9-123">Download the [Azure Dev Spaces extension](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds) for VS Code.</span></span> <span data-ttu-id="216c9-124">Click Install once on the extension's Marketplace page, and again in VS Code.</span><span class="sxs-lookup"><span data-stu-id="216c9-124">Click Install once on the extension's Marketplace page, and again in VS Code.</span></span>

## <a name="build-and-run-code-in-kubernetes"></a><span data-ttu-id="216c9-125">Build and run code in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="216c9-125">Build and run code in Kubernetes</span></span>

1. <span data-ttu-id="216c9-126">Download sample code from GitHub: [https://github.com/Azure/dev-spaces](https://github.com/Azure/dev-spaces)</span><span class="sxs-lookup"><span data-stu-id="216c9-126">Download sample code from GitHub: [https://github.com/Azure/dev-spaces](https://github.com/Azure/dev-spaces)</span></span> 
1. <span data-ttu-id="216c9-127">Change directory to the webfrontend folder: `cd dev-spaces/samples/nodejs/getting-started/webfrontend`</span><span class="sxs-lookup"><span data-stu-id="216c9-127">Change directory to the webfrontend folder: `cd dev-spaces/samples/nodejs/getting-started/webfrontend`</span></span>
1. <span data-ttu-id="216c9-128">Generate Docker and Helm chart assets: `azds prep --public`</span><span class="sxs-lookup"><span data-stu-id="216c9-128">Generate Docker and Helm chart assets: `azds prep --public`</span></span>
1. <span data-ttu-id="216c9-129">Build and run your code in AKS.</span><span class="sxs-lookup"><span data-stu-id="216c9-129">Build and run your code in AKS.</span></span> <span data-ttu-id="216c9-130">In the terminal window from the **webfrontend folder**, run this command: `azds up`</span><span class="sxs-lookup"><span data-stu-id="216c9-130">In the terminal window from the **webfrontend folder**, run this command: `azds up`</span></span>
1. <span data-ttu-id="216c9-131">Scan the console output for information about the URL that was created by the `up` command.</span><span class="sxs-lookup"><span data-stu-id="216c9-131">Scan the console output for information about the URL that was created by the `up` command.</span></span> <span data-ttu-id="216c9-132">It will be in the form:</span><span class="sxs-lookup"><span data-stu-id="216c9-132">It will be in the form:</span></span> 

   `Service 'webfrontend' port 'http' is available at <url>` 

   <span data-ttu-id="216c9-133">Open this URL in a browser window, and you should see the web app load.</span><span class="sxs-lookup"><span data-stu-id="216c9-133">Open this URL in a browser window, and you should see the web app load.</span></span> <span data-ttu-id="216c9-134">As the container executes, `stdout` and `stderr` output is streamed to the terminal window.</span><span class="sxs-lookup"><span data-stu-id="216c9-134">As the container executes, `stdout` and `stderr` output is streamed to the terminal window.</span></span>
   
   > [!Note]
   > <span data-ttu-id="216c9-135">On first run, it can take several minutes for public DNS to be ready.</span><span class="sxs-lookup"><span data-stu-id="216c9-135">On first run, it can take several minutes for public DNS to be ready.</span></span> <span data-ttu-id="216c9-136">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span><span class="sxs-lookup"><span data-stu-id="216c9-136">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span></span> <span data-ttu-id="216c9-137">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span><span class="sxs-lookup"><span data-stu-id="216c9-137">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span></span> <span data-ttu-id="216c9-138">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="216c9-138">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span> <span data-ttu-id="216c9-139">You can come back and try the public URL later when the DNS record is ready.</span><span class="sxs-lookup"><span data-stu-id="216c9-139">You can come back and try the public URL later when the DNS record is ready.</span></span>

### <a name="update-a-content-file"></a><span data-ttu-id="216c9-140">Update a content file</span><span class="sxs-lookup"><span data-stu-id="216c9-140">Update a content file</span></span>
<span data-ttu-id="216c9-141">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="216c9-141">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span></span>

1. <span data-ttu-id="216c9-142">Locate the file `./public/index.html` and make an edit to the HTML.</span><span class="sxs-lookup"><span data-stu-id="216c9-142">Locate the file `./public/index.html` and make an edit to the HTML.</span></span> <span data-ttu-id="216c9-143">For example, change the page's background color to a shade of blue:</span><span class="sxs-lookup"><span data-stu-id="216c9-143">For example, change the page's background color to a shade of blue:</span></span>

    ```html
    <body style="background-color: #95B9C7; margin-left:10px; margin-right:10px;">
    ```

1. <span data-ttu-id="216c9-144">Save the file.</span><span class="sxs-lookup"><span data-stu-id="216c9-144">Save the file.</span></span> <span data-ttu-id="216c9-145">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span><span class="sxs-lookup"><span data-stu-id="216c9-145">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span></span>
1. <span data-ttu-id="216c9-146">Go to your browser and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="216c9-146">Go to your browser and refresh the page.</span></span> <span data-ttu-id="216c9-147">You should see your color update.</span><span class="sxs-lookup"><span data-stu-id="216c9-147">You should see your color update.</span></span>

<span data-ttu-id="216c9-148">What happened?</span><span class="sxs-lookup"><span data-stu-id="216c9-148">What happened?</span></span> <span data-ttu-id="216c9-149">Edits to content files, like HTML and CSS, don't require the Node.js process to restart, so an active `azds up` command will automatically sync any modified content files directly into the running container in Azure, thereby providing a fast way to see your content edits.</span><span class="sxs-lookup"><span data-stu-id="216c9-149">Edits to content files, like HTML and CSS, don't require the Node.js process to restart, so an active `azds up` command will automatically sync any modified content files directly into the running container in Azure, thereby providing a fast way to see your content edits.</span></span>

### <a name="test-from-a-mobile-device"></a><span data-ttu-id="216c9-150">Test from a mobile device</span><span class="sxs-lookup"><span data-stu-id="216c9-150">Test from a mobile device</span></span>
<span data-ttu-id="216c9-151">Open the web app on a mobile device using the public URL for webfrontend.</span><span class="sxs-lookup"><span data-stu-id="216c9-151">Open the web app on a mobile device using the public URL for webfrontend.</span></span> <span data-ttu-id="216c9-152">You may want to copy and send the URL from your desktop to your device to save you from entering the long address.</span><span class="sxs-lookup"><span data-stu-id="216c9-152">You may want to copy and send the URL from your desktop to your device to save you from entering the long address.</span></span> <span data-ttu-id="216c9-153">When the web app loads in your mobile device, you will notice that the UI does not display properly on a small device.</span><span class="sxs-lookup"><span data-stu-id="216c9-153">When the web app loads in your mobile device, you will notice that the UI does not display properly on a small device.</span></span>

<span data-ttu-id="216c9-154">To fix this, you'll add a `viewport` meta tag:</span><span class="sxs-lookup"><span data-stu-id="216c9-154">To fix this, you'll add a `viewport` meta tag:</span></span>
1. <span data-ttu-id="216c9-155">Open the file `./public/index.html`</span><span class="sxs-lookup"><span data-stu-id="216c9-155">Open the file `./public/index.html`</span></span>
1. <span data-ttu-id="216c9-156">Add a `viewport` meta tag in the existing `head` element:</span><span class="sxs-lookup"><span data-stu-id="216c9-156">Add a `viewport` meta tag in the existing `head` element:</span></span>

    ```html
    <head>
        <!-- Add this line -->
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    ```

1. <span data-ttu-id="216c9-157">Save the file.</span><span class="sxs-lookup"><span data-stu-id="216c9-157">Save the file.</span></span>
1. <span data-ttu-id="216c9-158">Refresh your device's browser.</span><span class="sxs-lookup"><span data-stu-id="216c9-158">Refresh your device's browser.</span></span> <span data-ttu-id="216c9-159">You should now see the web app rendered correctly.</span><span class="sxs-lookup"><span data-stu-id="216c9-159">You should now see the web app rendered correctly.</span></span> 

<span data-ttu-id="216c9-160">This is an example of how some problems just aren't found until you test on the devices where an app is meant to be used.</span><span class="sxs-lookup"><span data-stu-id="216c9-160">This is an example of how some problems just aren't found until you test on the devices where an app is meant to be used.</span></span> <span data-ttu-id="216c9-161">With Azure Dev Spaces, you can rapidly iterate on your code and validate any changes on target devices.</span><span class="sxs-lookup"><span data-stu-id="216c9-161">With Azure Dev Spaces, you can rapidly iterate on your code and validate any changes on target devices.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="216c9-162">Update a code file</span><span class="sxs-lookup"><span data-stu-id="216c9-162">Update a code file</span></span>
<span data-ttu-id="216c9-163">Updating server-side code files requires a little more work, because a Node.js app needs to restart.</span><span class="sxs-lookup"><span data-stu-id="216c9-163">Updating server-side code files requires a little more work, because a Node.js app needs to restart.</span></span>

1. <span data-ttu-id="216c9-164">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span><span class="sxs-lookup"><span data-stu-id="216c9-164">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span></span>
1. <span data-ttu-id="216c9-165">Open the code file named `server.js`, and edit service's hello message:</span><span class="sxs-lookup"><span data-stu-id="216c9-165">Open the code file named `server.js`, and edit service's hello message:</span></span> 

    ```javascript
    res.send('Hello from webfrontend running in Azure!');
    ```

3. <span data-ttu-id="216c9-166">Save the file.</span><span class="sxs-lookup"><span data-stu-id="216c9-166">Save the file.</span></span>
1. <span data-ttu-id="216c9-167">Run  `azds up` in the terminal window.</span><span class="sxs-lookup"><span data-stu-id="216c9-167">Run  `azds up` in the terminal window.</span></span> 

<span data-ttu-id="216c9-168">This rebuilds the container image and redeploys the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="216c9-168">This rebuilds the container image and redeploys the Helm chart.</span></span> <span data-ttu-id="216c9-169">Reload the browser page to see your code changes take effect.</span><span class="sxs-lookup"><span data-stu-id="216c9-169">Reload the browser page to see your code changes take effect.</span></span>

<span data-ttu-id="216c9-170">But there is an even *faster method* for developing code, which you'll explore in the next section.</span><span class="sxs-lookup"><span data-stu-id="216c9-170">But there is an even *faster method* for developing code, which you'll explore in the next section.</span></span> 

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="216c9-171">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="216c9-171">Debug a container in Kubernetes</span></span>

<span data-ttu-id="216c9-172">In this section, you'll use VS Code to directly debug our container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="216c9-172">In this section, you'll use VS Code to directly debug our container running in Azure.</span></span> <span data-ttu-id="216c9-173">You'll also learn how to get a faster edit-run-test loop.</span><span class="sxs-lookup"><span data-stu-id="216c9-173">You'll also learn how to get a faster edit-run-test loop.</span></span>

![](./media/common/edit-refresh-see.png)

### <a name="initialize-debug-assets-with-the-vs-code-extension"></a><span data-ttu-id="216c9-174">Initialize debug assets with the VS Code extension</span><span class="sxs-lookup"><span data-stu-id="216c9-174">Initialize debug assets with the VS Code extension</span></span>
<span data-ttu-id="216c9-175">You first need to configure your code project so VS Code will communicate with our dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="216c9-175">You first need to configure your code project so VS Code will communicate with our dev space in Azure.</span></span> <span data-ttu-id="216c9-176">The VS Code extension for Azure Dev Spaces provides a helper command to set up debug configuration.</span><span class="sxs-lookup"><span data-stu-id="216c9-176">The VS Code extension for Azure Dev Spaces provides a helper command to set up debug configuration.</span></span> 

<span data-ttu-id="216c9-177">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span><span class="sxs-lookup"><span data-stu-id="216c9-177">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span></span>

<span data-ttu-id="216c9-178">This adds debug configuration for Azure Dev Spaces under the `.vscode` folder.</span><span class="sxs-lookup"><span data-stu-id="216c9-178">This adds debug configuration for Azure Dev Spaces under the `.vscode` folder.</span></span> <span data-ttu-id="216c9-179">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span><span class="sxs-lookup"><span data-stu-id="216c9-179">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span></span>

![](./media/common/command-palette.png)

### <a name="select-the-azds-debug-configuration"></a><span data-ttu-id="216c9-180">Select the AZDS debug configuration</span><span class="sxs-lookup"><span data-stu-id="216c9-180">Select the AZDS debug configuration</span></span>
1. <span data-ttu-id="216c9-181">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="216c9-181">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span>
1. <span data-ttu-id="216c9-182">Select **Launch Program (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="216c9-182">Select **Launch Program (AZDS)** as the active debug configuration.</span></span>

![](media/get-started-node/debug-configuration-nodejs2.png)

> [!Note]
> <span data-ttu-id="216c9-183">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="216c9-183">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span></span>

### <a name="debug-the-container-in-kubernetes"></a><span data-ttu-id="216c9-184">Debug the container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="216c9-184">Debug the container in Kubernetes</span></span>
<span data-ttu-id="216c9-185">Hit **F5** to debug your code in Kubernetes!</span><span class="sxs-lookup"><span data-stu-id="216c9-185">Hit **F5** to debug your code in Kubernetes!</span></span>

<span data-ttu-id="216c9-186">Similar to the `up` command, code is synced to the dev space when you start debugging, and a container is built and deployed to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="216c9-186">Similar to the `up` command, code is synced to the dev space when you start debugging, and a container is built and deployed to Kubernetes.</span></span> <span data-ttu-id="216c9-187">This time, the debugger is attached to the remote container.</span><span class="sxs-lookup"><span data-stu-id="216c9-187">This time, the debugger is attached to the remote container.</span></span>

> [!Tip]
> <span data-ttu-id="216c9-188">The VS Code status bar will display a clickable URL.</span><span class="sxs-lookup"><span data-stu-id="216c9-188">The VS Code status bar will display a clickable URL.</span></span>

<span data-ttu-id="216c9-189">Set a breakpoint in a server-side code file, for example within the `app.get('/api'...` in  `server.js`.</span><span class="sxs-lookup"><span data-stu-id="216c9-189">Set a breakpoint in a server-side code file, for example within the `app.get('/api'...` in  `server.js`.</span></span> <span data-ttu-id="216c9-190">Refresh the browser page, or press the 'Say It Again' button, and you should hit the breakpoint and be able to step through code.</span><span class="sxs-lookup"><span data-stu-id="216c9-190">Refresh the browser page, or press the 'Say It Again' button, and you should hit the breakpoint and be able to step through code.</span></span>

<span data-ttu-id="216c9-191">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span><span class="sxs-lookup"><span data-stu-id="216c9-191">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span></span>

### <a name="edit-code-and-refresh-the-debug-session"></a><span data-ttu-id="216c9-192">Edit code and refresh the debug session</span><span class="sxs-lookup"><span data-stu-id="216c9-192">Edit code and refresh the debug session</span></span>
<span data-ttu-id="216c9-193">With the debugger active, make a code edit; for example, modify the hello message again:</span><span class="sxs-lookup"><span data-stu-id="216c9-193">With the debugger active, make a code edit; for example, modify the hello message again:</span></span>

```javascript
app.get('/api', function (req, res) {
    res.send('**** Hello from webfrontend running in Azure! ****');
});
```

<span data-ttu-id="216c9-194">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="216c9-194">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span></span> 

![](media/get-started-node/debug-action-refresh-nodejs.png)

<span data-ttu-id="216c9-195">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will restart the Node.js process in between debug sessions to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="216c9-195">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will restart the Node.js process in between debug sessions to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="216c9-196">Refresh the web app in the browser, or press the *Say It Again* button.</span><span class="sxs-lookup"><span data-stu-id="216c9-196">Refresh the web app in the browser, or press the *Say It Again* button.</span></span> <span data-ttu-id="216c9-197">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="216c9-197">You should see your custom message appear in the UI.</span></span>

### <a name="use-nodemon-to-develop-even-faster"></a><span data-ttu-id="216c9-198">Use NodeMon to develop even faster</span><span class="sxs-lookup"><span data-stu-id="216c9-198">Use NodeMon to develop even faster</span></span>

<span data-ttu-id="216c9-199">The sample `webfrontend` project was configured to use [nodemon](https://nodemon.io/), a popular tool for speeding up Node.js development that is fully compatible with Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="216c9-199">The sample `webfrontend` project was configured to use [nodemon](https://nodemon.io/), a popular tool for speeding up Node.js development that is fully compatible with Azure Dev Spaces.</span></span>

<span data-ttu-id="216c9-200">Try the following steps:</span><span class="sxs-lookup"><span data-stu-id="216c9-200">Try the following steps:</span></span>
1. <span data-ttu-id="216c9-201">Stop the VS Code debugger.</span><span class="sxs-lookup"><span data-stu-id="216c9-201">Stop the VS Code debugger.</span></span>
1. <span data-ttu-id="216c9-202">Click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="216c9-202">Click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span> 
1. <span data-ttu-id="216c9-203">Select **Attach (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="216c9-203">Select **Attach (AZDS)** as the active debug configuration.</span></span>
1. <span data-ttu-id="216c9-204">Hit F5.</span><span class="sxs-lookup"><span data-stu-id="216c9-204">Hit F5.</span></span>

<span data-ttu-id="216c9-205">In this configuration, the container is configured to start *nodemon*.</span><span class="sxs-lookup"><span data-stu-id="216c9-205">In this configuration, the container is configured to start *nodemon*.</span></span> <span data-ttu-id="216c9-206">When server code edits are made, *nodemon* automatically restarts the Node process, just like it does when you develop locally.</span><span class="sxs-lookup"><span data-stu-id="216c9-206">When server code edits are made, *nodemon* automatically restarts the Node process, just like it does when you develop locally.</span></span> 
1. <span data-ttu-id="216c9-207">Edit the hello message again in `server.js`, and save the file.</span><span class="sxs-lookup"><span data-stu-id="216c9-207">Edit the hello message again in `server.js`, and save the file.</span></span>
1. <span data-ttu-id="216c9-208">Refresh the browser, or click the *Say It Again* button, to see your changes take effect!</span><span class="sxs-lookup"><span data-stu-id="216c9-208">Refresh the browser, or click the *Say It Again* button, to see your changes take effect!</span></span>

<span data-ttu-id="216c9-209">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span><span class="sxs-lookup"><span data-stu-id="216c9-209">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span></span>

## <a name="next-steps"></a><span data-ttu-id="216c9-210">Next steps</span><span class="sxs-lookup"><span data-stu-id="216c9-210">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="216c9-211">Working with multiple containers and team development</span><span class="sxs-lookup"><span data-stu-id="216c9-211">Working with multiple containers and team development</span></span>](team-development-nodejs.md)
