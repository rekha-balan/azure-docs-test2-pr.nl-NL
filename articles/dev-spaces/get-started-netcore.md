---
title: Create a Kubernetes dev space in the cloud using .NET Core and VS Code| Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 07/09/2018
ms.topic: tutorial
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: douge
ms.openlocfilehash: 0055276e8ce6ba6e22b8c2e664b3d2ae58b12345
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868560"
---
# <a name="get-started-on-azure-dev-spaces-with-net-core"></a><span data-ttu-id="bda1c-104">Get Started on Azure Dev Spaces with .NET Core</span><span class="sxs-lookup"><span data-stu-id="bda1c-104">Get Started on Azure Dev Spaces with .NET Core</span></span>

[!INCLUDE [](includes/learning-objectives.md)]

[!INCLUDE [](includes/see-troubleshooting.md)]

<span data-ttu-id="bda1c-105">You're now ready to create a Kubernetes-based dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="bda1c-105">You're now ready to create a Kubernetes-based dev space in Azure.</span></span>

[!INCLUDE [](includes/portal-aks-cluster.md)]

## <a name="install-the-azure-cli"></a><span data-ttu-id="bda1c-106">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="bda1c-106">Install the Azure CLI</span></span>
<span data-ttu-id="bda1c-107">Azure Dev Spaces requires minimal local machine setup.</span><span class="sxs-lookup"><span data-stu-id="bda1c-107">Azure Dev Spaces requires minimal local machine setup.</span></span> <span data-ttu-id="bda1c-108">Most of your dev space's configuration gets stored in the cloud, and is shareable with other users.</span><span class="sxs-lookup"><span data-stu-id="bda1c-108">Most of your dev space's configuration gets stored in the cloud, and is shareable with other users.</span></span> <span data-ttu-id="bda1c-109">Your local machine can run Windows, Mac, or Linux.</span><span class="sxs-lookup"><span data-stu-id="bda1c-109">Your local machine can run Windows, Mac, or Linux.</span></span> <span data-ttu-id="bda1c-110">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span><span class="sxs-lookup"><span data-stu-id="bda1c-110">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span></span>

<span data-ttu-id="bda1c-111">Start by downloading and running the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="bda1c-111">Start by downloading and running the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bda1c-112">If you already have the Azure CLI installed, make sure you are using version 2.0.43 or higher.</span><span class="sxs-lookup"><span data-stu-id="bda1c-112">If you already have the Azure CLI installed, make sure you are using version 2.0.43 or higher.</span></span>

[!INCLUDE [](includes/sign-into-azure.md)]

[!INCLUDE [](includes/use-dev-spaces.md)]

[!INCLUDE [](includes/install-vscode-extension.md)]

<span data-ttu-id="bda1c-113">While you're waiting for the cluster to be created, you can start developing code.</span><span class="sxs-lookup"><span data-stu-id="bda1c-113">While you're waiting for the cluster to be created, you can start developing code.</span></span>

## <a name="create-a-web-app-running-in-a-container"></a><span data-ttu-id="bda1c-114">Create a web app running in a container</span><span class="sxs-lookup"><span data-stu-id="bda1c-114">Create a web app running in a container</span></span>

<span data-ttu-id="bda1c-115">In this section, you'll create a ASP.NET Core web app and get it running in a container in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bda1c-115">In this section, you'll create a ASP.NET Core web app and get it running in a container in Kubernetes.</span></span>

### <a name="create-an-aspnet-core-web-app"></a><span data-ttu-id="bda1c-116">Create an ASP.NET Core web app</span><span class="sxs-lookup"><span data-stu-id="bda1c-116">Create an ASP.NET Core web app</span></span>
<span data-ttu-id="bda1c-117">If you have [.NET Core](https://www.microsoft.com/net) installed, you can quickly create an ASP.NET Core Web App in a folder named `webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="bda1c-117">If you have [.NET Core](https://www.microsoft.com/net) installed, you can quickly create an ASP.NET Core Web App in a folder named `webfrontend`.</span></span>
    
```cmd
dotnet new mvc --name webfrontend
```

<span data-ttu-id="bda1c-118">Or, **download sample code from GitHub** by navigating to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository to your local environment.</span><span class="sxs-lookup"><span data-stu-id="bda1c-118">Or, **download sample code from GitHub** by navigating to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository to your local environment.</span></span> <span data-ttu-id="bda1c-119">The code for this guide is in `samples/dotnetcore/getting-started/webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="bda1c-119">The code for this guide is in `samples/dotnetcore/getting-started/webfrontend`.</span></span>

[!INCLUDE [](includes/azds-prep.md)]

[!INCLUDE [](includes/build-run-k8s-cli.md)]

### <a name="update-a-content-file"></a><span data-ttu-id="bda1c-120">Update a content file</span><span class="sxs-lookup"><span data-stu-id="bda1c-120">Update a content file</span></span>
<span data-ttu-id="bda1c-121">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="bda1c-121">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span></span>

1. <span data-ttu-id="bda1c-122">Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML.</span><span class="sxs-lookup"><span data-stu-id="bda1c-122">Locate the file `./Views/Home/Index.cshtml` and make an edit to the HTML.</span></span> <span data-ttu-id="bda1c-123">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span><span class="sxs-lookup"><span data-stu-id="bda1c-123">For example, change line 70 that reads `<h2>Application uses</h2>` to something like: `<h2>Hello k8s in Azure!</h2>`</span></span>
1. <span data-ttu-id="bda1c-124">Save the file.</span><span class="sxs-lookup"><span data-stu-id="bda1c-124">Save the file.</span></span> <span data-ttu-id="bda1c-125">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span><span class="sxs-lookup"><span data-stu-id="bda1c-125">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span></span>
1. <span data-ttu-id="bda1c-126">Go to your browser and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="bda1c-126">Go to your browser and refresh the page.</span></span> <span data-ttu-id="bda1c-127">You should see the web page display the updated HTML.</span><span class="sxs-lookup"><span data-stu-id="bda1c-127">You should see the web page display the updated HTML.</span></span>

<span data-ttu-id="bda1c-128">What happened?</span><span class="sxs-lookup"><span data-stu-id="bda1c-128">What happened?</span></span> <span data-ttu-id="bda1c-129">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active `azds up` command automatically syncs any modified content files into the running container in Azure, so you can see your content edits right away.</span><span class="sxs-lookup"><span data-stu-id="bda1c-129">Edits to content files, like HTML and CSS, don't require recompilation in a .NET Core web app, so an active `azds up` command automatically syncs any modified content files into the running container in Azure, so you can see your content edits right away.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="bda1c-130">Update a code file</span><span class="sxs-lookup"><span data-stu-id="bda1c-130">Update a code file</span></span>
<span data-ttu-id="bda1c-131">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span><span class="sxs-lookup"><span data-stu-id="bda1c-131">Updating code files requires a little more work, because a .NET Core app needs to rebuild and produce updated application binaries.</span></span>

1. <span data-ttu-id="bda1c-132">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span><span class="sxs-lookup"><span data-stu-id="bda1c-132">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span></span>
1. <span data-ttu-id="bda1c-133">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span><span class="sxs-lookup"><span data-stu-id="bda1c-133">Open the code file named `Controllers/HomeController.cs`, and edit the message that the About page will display: `ViewData["Message"] = "Your application description page.";`</span></span>
1. <span data-ttu-id="bda1c-134">Save the file.</span><span class="sxs-lookup"><span data-stu-id="bda1c-134">Save the file.</span></span>
1. <span data-ttu-id="bda1c-135">Run  `azds up` in the terminal window.</span><span class="sxs-lookup"><span data-stu-id="bda1c-135">Run  `azds up` in the terminal window.</span></span> 

<span data-ttu-id="bda1c-136">This command rebuilds the container image and redeploys the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="bda1c-136">This command rebuilds the container image and redeploys the Helm chart.</span></span> <span data-ttu-id="bda1c-137">To see your code changes take effect in the running application, go to the About menu in the web app.</span><span class="sxs-lookup"><span data-stu-id="bda1c-137">To see your code changes take effect in the running application, go to the About menu in the web app.</span></span>


<span data-ttu-id="bda1c-138">But there is an even *faster method* for developing code, which you'll explore in the next section.</span><span class="sxs-lookup"><span data-stu-id="bda1c-138">But there is an even *faster method* for developing code, which you'll explore in the next section.</span></span> 

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="bda1c-139">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bda1c-139">Debug a container in Kubernetes</span></span>

[!INCLUDE [](includes/debug-intro.md)]

[!INCLUDE [](includes/init-debug-assets-vscode.md)]


### <a name="select-the-azds-debug-configuration"></a><span data-ttu-id="bda1c-140">Select the AZDS debug configuration</span><span class="sxs-lookup"><span data-stu-id="bda1c-140">Select the AZDS debug configuration</span></span>
1. <span data-ttu-id="bda1c-141">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="bda1c-141">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span>
1. <span data-ttu-id="bda1c-142">Select **.NET Core Launch (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="bda1c-142">Select **.NET Core Launch (AZDS)** as the active debug configuration.</span></span>

![](media/get-started-netcore/debug-configuration.png)

> [!Note]
> <span data-ttu-id="bda1c-143">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="bda1c-143">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span></span> <span data-ttu-id="bda1c-144">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span><span class="sxs-lookup"><span data-stu-id="bda1c-144">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span></span>


### <a name="debug-the-container-in-kubernetes"></a><span data-ttu-id="bda1c-145">Debug the container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="bda1c-145">Debug the container in Kubernetes</span></span>
<span data-ttu-id="bda1c-146">Hit **F5** to debug your code in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bda1c-146">Hit **F5** to debug your code in Kubernetes.</span></span>

<span data-ttu-id="bda1c-147">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="bda1c-147">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span></span> <span data-ttu-id="bda1c-148">This time, of course, the debugger is attached to the remote container.</span><span class="sxs-lookup"><span data-stu-id="bda1c-148">This time, of course, the debugger is attached to the remote container.</span></span>

[!INCLUDE [](includes/tip-vscode-status-bar-url.md)]

<span data-ttu-id="bda1c-149">Set a breakpoint in a server-side code file, for example within the `Index()` function in the `Controllers/HomeController.cs` source file.</span><span class="sxs-lookup"><span data-stu-id="bda1c-149">Set a breakpoint in a server-side code file, for example within the `Index()` function in the `Controllers/HomeController.cs` source file.</span></span> <span data-ttu-id="bda1c-150">Refreshing the browser page causes the breakpoint to hit.</span><span class="sxs-lookup"><span data-stu-id="bda1c-150">Refreshing the browser page causes the breakpoint to hit.</span></span>

<span data-ttu-id="bda1c-151">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span><span class="sxs-lookup"><span data-stu-id="bda1c-151">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span></span>

### <a name="edit-code-and-refresh"></a><span data-ttu-id="bda1c-152">Edit code and refresh</span><span class="sxs-lookup"><span data-stu-id="bda1c-152">Edit code and refresh</span></span>
<span data-ttu-id="bda1c-153">With the debugger active, make a code edit.</span><span class="sxs-lookup"><span data-stu-id="bda1c-153">With the debugger active, make a code edit.</span></span> <span data-ttu-id="bda1c-154">For example, modify the About page's message in `Controllers/HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="bda1c-154">For example, modify the About page's message in `Controllers/HomeController.cs`.</span></span> 

```csharp
public IActionResult About()
{
    ViewData["Message"] = "My custom message in the About page.";
    return View();
}
```

<span data-ttu-id="bda1c-155">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="bda1c-155">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span></span> 

![](media/get-started-netcore/debug-action-refresh.png)

<span data-ttu-id="bda1c-156">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="bda1c-156">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="bda1c-157">Refresh the web app in the browser, and go to the About page.</span><span class="sxs-lookup"><span data-stu-id="bda1c-157">Refresh the web app in the browser, and go to the About page.</span></span> <span data-ttu-id="bda1c-158">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="bda1c-158">You should see your custom message appear in the UI.</span></span>

<span data-ttu-id="bda1c-159">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span><span class="sxs-lookup"><span data-stu-id="bda1c-159">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span></span> <span data-ttu-id="bda1c-160">Next, you'll see how you can create and call a second container.</span><span class="sxs-lookup"><span data-stu-id="bda1c-160">Next, you'll see how you can create and call a second container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bda1c-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="bda1c-161">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bda1c-162">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="bda1c-162">Learn about team development</span></span>](team-development-netcore.md)
