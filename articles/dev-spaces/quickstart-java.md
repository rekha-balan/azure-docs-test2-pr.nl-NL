---
title: Create a Kubernetes dev space in the cloud | Microsoft Docs
titleSuffix: Azure Dev Spaces
author: stepro
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
ms.author: stephpr
ms.date: 08/01/2018
ms.topic: quickstart
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: mmontwil
ms.openlocfilehash: f1068243605763953903cbd9a6aa5b99205ae279
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867851"
---
# <a name="quickstart-create-a-kubernetes-dev-space-with-azure-dev-spaces-java-and-vs-code"></a><span data-ttu-id="bdc60-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (Java and VS Code)</span><span class="sxs-lookup"><span data-stu-id="bdc60-104">Quickstart: Create a Kubernetes dev space with Azure Dev Spaces (Java and VS Code)</span></span>

<span data-ttu-id="bdc60-105">In this guide, you will learn how to:</span><span class="sxs-lookup"><span data-stu-id="bdc60-105">In this guide, you will learn how to:</span></span>

- <span data-ttu-id="bdc60-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc60-106">Set up Azure Dev Spaces with a managed Kubernetes cluster in Azure.</span></span>
- <span data-ttu-id="bdc60-107">Iteratively develop code in containers using VS Code and the command line.</span><span class="sxs-lookup"><span data-stu-id="bdc60-107">Iteratively develop code in containers using VS Code and the command line.</span></span>
- <span data-ttu-id="bdc60-108">Debug the code in your dev space from VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdc60-108">Debug the code in your dev space from VS Code.</span></span>

> [!Note]
> <span data-ttu-id="bdc60-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span><span class="sxs-lookup"><span data-stu-id="bdc60-109">**If you get stuck** at any time, see the [Troubleshooting](troubleshooting.md) section, or post a comment on this page.</span></span> <span data-ttu-id="bdc60-110">You can also try the more detailed [tutorial](get-started-netcore.md).</span><span class="sxs-lookup"><span data-stu-id="bdc60-110">You can also try the more detailed [tutorial](get-started-netcore.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdc60-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bdc60-111">Prerequisites</span></span>

- <span data-ttu-id="bdc60-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="bdc60-112">An Azure subscription.</span></span> <span data-ttu-id="bdc60-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="bdc60-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/free).</span></span>
- <span data-ttu-id="bdc60-114">A [Kubernetes cluster](https://ms.portal.azure.com/#create/microsoft.aks) running Kubernetes 1.10.3, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with **Http Application Routing** enabled.</span><span class="sxs-lookup"><span data-stu-id="bdc60-114">A [Kubernetes cluster](https://ms.portal.azure.com/#create/microsoft.aks) running Kubernetes 1.10.3, in the EastUS, CentralUS, WestUS2, WestEurope, CanadaCentral, or CanadaEast region, with **Http Application Routing** enabled.</span></span>

  ![Be sure to enable Http Application Routing.](media/common/Kubernetes-Create-Cluster-3.PNG)

- <span data-ttu-id="bdc60-116">[Visual Studio Code](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="bdc60-116">[Visual Studio Code](https://code.visualstudio.com/download).</span></span>

## <a name="set-up-azure-dev-spaces"></a><span data-ttu-id="bdc60-117">Set up Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="bdc60-117">Set up Azure Dev Spaces</span></span>

1. <span data-ttu-id="bdc60-118">Install the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) (version 2.0.43 or higher).</span><span class="sxs-lookup"><span data-stu-id="bdc60-118">Install the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest) (version 2.0.43 or higher).</span></span>
1. <span data-ttu-id="bdc60-119">Set up Dev Spaces on your AKS cluster: `az aks use-dev-spaces -g MyResourceGroup -n MyAKS`</span><span class="sxs-lookup"><span data-stu-id="bdc60-119">Set up Dev Spaces on your AKS cluster: `az aks use-dev-spaces -g MyResourceGroup -n MyAKS`</span></span>
1. <span data-ttu-id="bdc60-120">Download the [Azure Dev Spaces extension](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds) for VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdc60-120">Download the [Azure Dev Spaces extension](https://marketplace.visualstudio.com/items?itemName=azuredevspaces.azds) for VS Code.</span></span> <span data-ttu-id="bdc60-121">Click Install once on the extension's Marketplace page, and again in VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdc60-121">Click Install once on the extension's Marketplace page, and again in VS Code.</span></span>
1. <span data-ttu-id="bdc60-122">Download the [Java Debugger for Azure Dev Spaces](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debugger-azds) extension for VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdc60-122">Download the [Java Debugger for Azure Dev Spaces](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debugger-azds) extension for VS Code.</span></span> <span data-ttu-id="bdc60-123">Click Install once on the extension's Marketplace page, and again in VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdc60-123">Click Install once on the extension's Marketplace page, and again in VS Code.</span></span>

## <a name="build-and-run-code-in-kubernetes"></a><span data-ttu-id="bdc60-124">Build and run code in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bdc60-124">Build and run code in Kubernetes</span></span>

1. <span data-ttu-id="bdc60-125">Download sample code from GitHub: [https://github.com/Azure/dev-spaces](https://github.com/Azure/dev-spaces)</span><span class="sxs-lookup"><span data-stu-id="bdc60-125">Download sample code from GitHub: [https://github.com/Azure/dev-spaces](https://github.com/Azure/dev-spaces)</span></span> 
1. <span data-ttu-id="bdc60-126">Change directory to the webfrontend folder: `cd dev-spaces/samples/java/getting-started/webfrontend`</span><span class="sxs-lookup"><span data-stu-id="bdc60-126">Change directory to the webfrontend folder: `cd dev-spaces/samples/java/getting-started/webfrontend`</span></span>
1. <span data-ttu-id="bdc60-127">Generate Docker and Helm chart assets: `azds prep --public`</span><span class="sxs-lookup"><span data-stu-id="bdc60-127">Generate Docker and Helm chart assets: `azds prep --public`</span></span>
1. <span data-ttu-id="bdc60-128">Build and run your code in AKS.</span><span class="sxs-lookup"><span data-stu-id="bdc60-128">Build and run your code in AKS.</span></span> <span data-ttu-id="bdc60-129">In the terminal window from the **webfrontend folder**, run this command: `azds up`</span><span class="sxs-lookup"><span data-stu-id="bdc60-129">In the terminal window from the **webfrontend folder**, run this command: `azds up`</span></span>
1. <span data-ttu-id="bdc60-130">Scan the console output for information about the URL that was created by the `up` command.</span><span class="sxs-lookup"><span data-stu-id="bdc60-130">Scan the console output for information about the URL that was created by the `up` command.</span></span> <span data-ttu-id="bdc60-131">It will be in the form:</span><span class="sxs-lookup"><span data-stu-id="bdc60-131">It will be in the form:</span></span>

   `Service 'webfrontend' port 'http' is available at <url>`

   <span data-ttu-id="bdc60-132">Open this URL in a browser window, and you should see the web app load.</span><span class="sxs-lookup"><span data-stu-id="bdc60-132">Open this URL in a browser window, and you should see the web app load.</span></span>

   > [!Note]
   > <span data-ttu-id="bdc60-133">On first run, it can take several minutes for public DNS to be ready.</span><span class="sxs-lookup"><span data-stu-id="bdc60-133">On first run, it can take several minutes for public DNS to be ready.</span></span> <span data-ttu-id="bdc60-134">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span><span class="sxs-lookup"><span data-stu-id="bdc60-134">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span></span> <span data-ttu-id="bdc60-135">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span><span class="sxs-lookup"><span data-stu-id="bdc60-135">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span></span> <span data-ttu-id="bdc60-136">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc60-136">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span> <span data-ttu-id="bdc60-137">You can come back and try the public URL later when the DNS record is ready.</span><span class="sxs-lookup"><span data-stu-id="bdc60-137">You can come back and try the public URL later when the DNS record is ready.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="bdc60-138">Update a code file</span><span class="sxs-lookup"><span data-stu-id="bdc60-138">Update a code file</span></span>

1. <span data-ttu-id="bdc60-139">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span><span class="sxs-lookup"><span data-stu-id="bdc60-139">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span></span>
1. <span data-ttu-id="bdc60-140">Open the code file named `src/main/java/com/ms/sample/webfrontend/Application.java` and edit the greeting message: `return "Hello from webfrontend in Azure!";`</span><span class="sxs-lookup"><span data-stu-id="bdc60-140">Open the code file named `src/main/java/com/ms/sample/webfrontend/Application.java` and edit the greeting message: `return "Hello from webfrontend in Azure!";`</span></span>
1. <span data-ttu-id="bdc60-141">Save the file.</span><span class="sxs-lookup"><span data-stu-id="bdc60-141">Save the file.</span></span>
1. <span data-ttu-id="bdc60-142">Run  `azds up` in the terminal window.</span><span class="sxs-lookup"><span data-stu-id="bdc60-142">Run  `azds up` in the terminal window.</span></span>

<span data-ttu-id="bdc60-143">This command rebuilds the container image and redeploys the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="bdc60-143">This command rebuilds the container image and redeploys the Helm chart.</span></span> <span data-ttu-id="bdc60-144">To see your code changes take effect in the running application, simply refresh the browser.</span><span class="sxs-lookup"><span data-stu-id="bdc60-144">To see your code changes take effect in the running application, simply refresh the browser.</span></span>

<span data-ttu-id="bdc60-145">But there is an even *faster method* for developing code, which you'll explore in the next section.</span><span class="sxs-lookup"><span data-stu-id="bdc60-145">But there is an even *faster method* for developing code, which you'll explore in the next section.</span></span>

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="bdc60-146">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bdc60-146">Debug a container in Kubernetes</span></span>

<span data-ttu-id="bdc60-147">In this section, you'll use VS Code to directly debug your container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc60-147">In this section, you'll use VS Code to directly debug your container running in Azure.</span></span> <span data-ttu-id="bdc60-148">You'll also learn how to get a faster edit-run-test loop.</span><span class="sxs-lookup"><span data-stu-id="bdc60-148">You'll also learn how to get a faster edit-run-test loop.</span></span>

![](./media/common/edit-refresh-see.png)

### <a name="initialize-debug-assets-with-the-vs-code-extension"></a><span data-ttu-id="bdc60-149">Initialize debug assets with the VS Code extension</span><span class="sxs-lookup"><span data-stu-id="bdc60-149">Initialize debug assets with the VS Code extension</span></span>
<span data-ttu-id="bdc60-150">You first need to configure your code project so VS Code will communicate with the dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc60-150">You first need to configure your code project so VS Code will communicate with the dev space in Azure.</span></span> <span data-ttu-id="bdc60-151">The VS Code extension for Azure Dev Spaces provides a helper command to set up debug configuration.</span><span class="sxs-lookup"><span data-stu-id="bdc60-151">The VS Code extension for Azure Dev Spaces provides a helper command to set up debug configuration.</span></span>

<span data-ttu-id="bdc60-152">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span><span class="sxs-lookup"><span data-stu-id="bdc60-152">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span></span>

<span data-ttu-id="bdc60-153">This adds debug configuration for Azure Dev Spaces under the `.vscode` folder.</span><span class="sxs-lookup"><span data-stu-id="bdc60-153">This adds debug configuration for Azure Dev Spaces under the `.vscode` folder.</span></span>

![](./media/common/command-palette.png)

### <a name="select-the-azds-debug-configuration"></a><span data-ttu-id="bdc60-154">Select the AZDS debug configuration</span><span class="sxs-lookup"><span data-stu-id="bdc60-154">Select the AZDS debug configuration</span></span>
1. <span data-ttu-id="bdc60-155">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="bdc60-155">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span>
1. <span data-ttu-id="bdc60-156">Select **Launch Java Program (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="bdc60-156">Select **Launch Java Program (AZDS)** as the active debug configuration.</span></span>

![](media/get-started-java/debug-configuration.png)

> [!Note]
> <span data-ttu-id="bdc60-157">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="bdc60-157">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span></span> <span data-ttu-id="bdc60-158">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span><span class="sxs-lookup"><span data-stu-id="bdc60-158">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span></span>

### <a name="debug-the-container-in-kubernetes"></a><span data-ttu-id="bdc60-159">Debug the container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bdc60-159">Debug the container in Kubernetes</span></span>
<span data-ttu-id="bdc60-160">Hit **F5** to debug your code in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bdc60-160">Hit **F5** to debug your code in Kubernetes.</span></span>

<span data-ttu-id="bdc60-161">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bdc60-161">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span></span> <span data-ttu-id="bdc60-162">This time, of course, the debugger is attached to the remote container.</span><span class="sxs-lookup"><span data-stu-id="bdc60-162">This time, of course, the debugger is attached to the remote container.</span></span>

> [!Tip]
> <span data-ttu-id="bdc60-163">The VS Code status bar will display a clickable URL.</span><span class="sxs-lookup"><span data-stu-id="bdc60-163">The VS Code status bar will display a clickable URL.</span></span>

<span data-ttu-id="bdc60-164">Set a breakpoint in a server-side code file, for example within the `greeting()` function in the `src/main/java/com/ms/sample/webfrontend/Application.java` source file.</span><span class="sxs-lookup"><span data-stu-id="bdc60-164">Set a breakpoint in a server-side code file, for example within the `greeting()` function in the `src/main/java/com/ms/sample/webfrontend/Application.java` source file.</span></span> <span data-ttu-id="bdc60-165">Refreshing the browser page causes the breakpoint to be hit.</span><span class="sxs-lookup"><span data-stu-id="bdc60-165">Refreshing the browser page causes the breakpoint to be hit.</span></span>

<span data-ttu-id="bdc60-166">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span><span class="sxs-lookup"><span data-stu-id="bdc60-166">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span></span>

### <a name="edit-code-and-refresh"></a><span data-ttu-id="bdc60-167">Edit code and refresh</span><span class="sxs-lookup"><span data-stu-id="bdc60-167">Edit code and refresh</span></span>
<span data-ttu-id="bdc60-168">With the debugger active, make a code edit.</span><span class="sxs-lookup"><span data-stu-id="bdc60-168">With the debugger active, make a code edit.</span></span> <span data-ttu-id="bdc60-169">For example, modify the greeting in `src/main/java/com/ms/sample/webfrontend/Application.java`.</span><span class="sxs-lookup"><span data-stu-id="bdc60-169">For example, modify the greeting in `src/main/java/com/ms/sample/webfrontend/Application.java`.</span></span> 

```java
public String greeting()
{
    return "I'm debugging Java code in Azure!";
}
```

<span data-ttu-id="bdc60-170">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="bdc60-170">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span></span> 

![](media/get-started-java/debug-action-refresh.png)

<span data-ttu-id="bdc60-171">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="bdc60-171">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="bdc60-172">Refresh the web app in the browser.</span><span class="sxs-lookup"><span data-stu-id="bdc60-172">Refresh the web app in the browser.</span></span> <span data-ttu-id="bdc60-173">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="bdc60-173">You should see your custom message appear in the UI.</span></span>

<span data-ttu-id="bdc60-174">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span><span class="sxs-lookup"><span data-stu-id="bdc60-174">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdc60-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="bdc60-175">Next steps</span></span>

<span data-ttu-id="bdc60-176">Learn how Azure Dev Spaces helps you develop more complex apps across multiple containers, and how you can simplify collaborative development by working with different versions or branches of your code in different spaces.</span><span class="sxs-lookup"><span data-stu-id="bdc60-176">Learn how Azure Dev Spaces helps you develop more complex apps across multiple containers, and how you can simplify collaborative development by working with different versions or branches of your code in different spaces.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bdc60-177">Working with multiple containers and team development</span><span class="sxs-lookup"><span data-stu-id="bdc60-177">Working with multiple containers and team development</span></span>](team-development-java.md)