---
title: Create a Kubernetes dev space in the cloud using Java and VS Code| Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: stepro
ms.author: stephpr
ms.date: 08/01/2018
ms.topic: tutorial
description: Rapid Kubernetes development with containers and microservices on Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, containers
manager: mmontwil
ms.openlocfilehash: eb7892ab02b6a9760fdebd47db1fb31120ae7ecf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866043"
---
# <a name="get-started-on-azure-dev-spaces-with-java"></a><span data-ttu-id="4f2b6-104">Get Started on Azure Dev Spaces with Java</span><span class="sxs-lookup"><span data-stu-id="4f2b6-104">Get Started on Azure Dev Spaces with Java</span></span>

[!INCLUDE[](includes/learning-objectives.md)]

[!INCLUDE[](includes/see-troubleshooting.md)]

<span data-ttu-id="4f2b6-105">You're now ready to create a Kubernetes-based dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-105">You're now ready to create a Kubernetes-based dev space in Azure.</span></span>

[!INCLUDE[](includes/portal-aks-cluster.md)]

## <a name="install-the-azure-cli"></a><span data-ttu-id="4f2b6-106">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f2b6-106">Install the Azure CLI</span></span>
<span data-ttu-id="4f2b6-107">Azure Dev Spaces requires minimal local machine setup.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-107">Azure Dev Spaces requires minimal local machine setup.</span></span> <span data-ttu-id="4f2b6-108">Most of your dev space's configuration gets stored in the cloud, and is shareable with other users.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-108">Most of your dev space's configuration gets stored in the cloud, and is shareable with other users.</span></span> <span data-ttu-id="4f2b6-109">Start by downloading and running the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="4f2b6-109">Start by downloading and running the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f2b6-110">If you already have the Azure CLI installed, make sure you are using version 2.0.43 or higher.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-110">If you already have the Azure CLI installed, make sure you are using version 2.0.43 or higher.</span></span>

[!INCLUDE[](includes/sign-into-azure.md)]

[!INCLUDE[](includes/use-dev-spaces.md)]

[!INCLUDE[](includes/install-vscode-extension.md)]

<span data-ttu-id="4f2b6-111">In order to debug Java applications with Azure Dev Spaces, download and install the [Java Debugger for Azure Dev Spaces](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debugger-azds) extension for VS Code.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-111">In order to debug Java applications with Azure Dev Spaces, download and install the [Java Debugger for Azure Dev Spaces](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-debugger-azds) extension for VS Code.</span></span> <span data-ttu-id="4f2b6-112">Click Install once on the extension's Marketplace page, and again in VS Code.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-112">Click Install once on the extension's Marketplace page, and again in VS Code.</span></span>

<span data-ttu-id="4f2b6-113">While you're waiting for the cluster to be created, you can start developing code.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-113">While you're waiting for the cluster to be created, you can start developing code.</span></span>

## <a name="create-a-web-app-running-in-a-container"></a><span data-ttu-id="4f2b6-114">Create a web app running in a container</span><span class="sxs-lookup"><span data-stu-id="4f2b6-114">Create a web app running in a container</span></span>

<span data-ttu-id="4f2b6-115">In this section, you'll create a Java web application and get it running in a container in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-115">In this section, you'll create a Java web application and get it running in a container in Kubernetes.</span></span>

### <a name="create-a-java-web-app"></a><span data-ttu-id="4f2b6-116">Create a Java web app</span><span class="sxs-lookup"><span data-stu-id="4f2b6-116">Create a Java web app</span></span>
<span data-ttu-id="4f2b6-117">Download code from GitHub by navigating to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository to your local environment.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-117">Download code from GitHub by navigating to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository to your local environment.</span></span> <span data-ttu-id="4f2b6-118">The code for this guide is in `samples/java/getting-started/webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-118">The code for this guide is in `samples/java/getting-started/webfrontend`.</span></span>

[!INCLUDE[](includes/azds-prep.md)]

[!INCLUDE[](includes/build-run-k8s-cli.md)]

### <a name="update-a-content-file"></a><span data-ttu-id="4f2b6-119">Update a content file</span><span class="sxs-lookup"><span data-stu-id="4f2b6-119">Update a content file</span></span>
<span data-ttu-id="4f2b6-120">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-120">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span></span>

1. <span data-ttu-id="4f2b6-121">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span><span class="sxs-lookup"><span data-stu-id="4f2b6-121">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span></span>
1. <span data-ttu-id="4f2b6-122">Open the code file named `src/main/java/com/ms/sample/webfrontend/Application.java`, and edit the greeting message: `return "Hello from webfrontend in Azure!";`</span><span class="sxs-lookup"><span data-stu-id="4f2b6-122">Open the code file named `src/main/java/com/ms/sample/webfrontend/Application.java`, and edit the greeting message: `return "Hello from webfrontend in Azure!";`</span></span>
1. <span data-ttu-id="4f2b6-123">Save the file.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-123">Save the file.</span></span>
1. <span data-ttu-id="4f2b6-124">Run  `azds up` in the terminal window.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-124">Run  `azds up` in the terminal window.</span></span>

<span data-ttu-id="4f2b6-125">This command rebuilds the container image and redeploys the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-125">This command rebuilds the container image and redeploys the Helm chart.</span></span> <span data-ttu-id="4f2b6-126">To see your code changes take effect in the running application, simply refresh the browser.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-126">To see your code changes take effect in the running application, simply refresh the browser.</span></span>

<span data-ttu-id="4f2b6-127">But there is an even *faster method* for developing code, which you'll explore in the next section.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-127">But there is an even *faster method* for developing code, which you'll explore in the next section.</span></span> 

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="4f2b6-128">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4f2b6-128">Debug a container in Kubernetes</span></span>

[!INCLUDE[](includes/debug-intro.md)]

[!INCLUDE[](includes/init-debug-assets-vscode.md)]

### <a name="select-the-azds-debug-configuration"></a><span data-ttu-id="4f2b6-129">Select the AZDS debug configuration</span><span class="sxs-lookup"><span data-stu-id="4f2b6-129">Select the AZDS debug configuration</span></span>
1. <span data-ttu-id="4f2b6-130">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-130">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span>
1. <span data-ttu-id="4f2b6-131">Select **Launch Java Program (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-131">Select **Launch Java Program (AZDS)** as the active debug configuration.</span></span>

![](media/get-started-java/debug-configuration.png)

> [!Note]
> <span data-ttu-id="4f2b6-132">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-132">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have installed the VS Code extension for Azure Dev Spaces.</span></span> <span data-ttu-id="4f2b6-133">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-133">Be sure the workspace you opened in VS Code is the folder that contains azds.yaml.</span></span>

### <a name="debug-the-container-in-kubernetes"></a><span data-ttu-id="4f2b6-134">Debug the container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4f2b6-134">Debug the container in Kubernetes</span></span>
<span data-ttu-id="4f2b6-135">Hit **F5** to debug your code in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-135">Hit **F5** to debug your code in Kubernetes.</span></span>

<span data-ttu-id="4f2b6-136">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-136">As with the `up` command, code is synced to the dev space, and a container is built and deployed to Kubernetes.</span></span> <span data-ttu-id="4f2b6-137">This time, of course, the debugger is attached to the remote container.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-137">This time, of course, the debugger is attached to the remote container.</span></span>

[!INCLUDE[](includes/tip-vscode-status-bar-url.md)]

<span data-ttu-id="4f2b6-138">Set a breakpoint in a server-side code file, for example within the `greeting()` function in the `src/main/java/com/ms/sample/webfrontend/Application.java` source file.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-138">Set a breakpoint in a server-side code file, for example within the `greeting()` function in the `src/main/java/com/ms/sample/webfrontend/Application.java` source file.</span></span> <span data-ttu-id="4f2b6-139">Refreshing the browser page causes the breakpoint to hit.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-139">Refreshing the browser page causes the breakpoint to hit.</span></span>

<span data-ttu-id="4f2b6-140">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-140">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span></span>

### <a name="edit-code-and-refresh"></a><span data-ttu-id="4f2b6-141">Edit code and refresh</span><span class="sxs-lookup"><span data-stu-id="4f2b6-141">Edit code and refresh</span></span>
<span data-ttu-id="4f2b6-142">With the debugger active, make a code edit.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-142">With the debugger active, make a code edit.</span></span> <span data-ttu-id="4f2b6-143">For example, modify the greeting in `src/main/java/com/ms/sample/webfrontend/Application.java`.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-143">For example, modify the greeting in `src/main/java/com/ms/sample/webfrontend/Application.java`.</span></span> 

```java
public String greeting()
{
    return "I'm debugging Java code in Azure!";
}
```

<span data-ttu-id="4f2b6-144">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-144">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span></span>

![](media/get-started-java/debug-action-refresh.png)

<span data-ttu-id="4f2b6-145">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-145">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will incrementally recompile code within the existing container to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="4f2b6-146">Refresh the web app in the browser.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-146">Refresh the web app in the browser.</span></span> <span data-ttu-id="4f2b6-147">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-147">You should see your custom message appear in the UI.</span></span>

<span data-ttu-id="4f2b6-148">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span><span class="sxs-lookup"><span data-stu-id="4f2b6-148">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span></span> <span data-ttu-id="4f2b6-149">Next, you'll see how you can create and call a second container.</span><span class="sxs-lookup"><span data-stu-id="4f2b6-149">Next, you'll see how you can create and call a second container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f2b6-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="4f2b6-150">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4f2b6-151">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="4f2b6-151">Learn about team development</span></span>](team-development-java.md)