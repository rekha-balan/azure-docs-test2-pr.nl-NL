---
title: Create a Kubernetes Node.js development environment in the cloud with VS Code | Microsoft Docs
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
ms.openlocfilehash: f441f18ab72485feca9356f7218a35b2c351dd40
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870232"
---
# <a name="get-started-on-azure-dev-spaces-with-nodejs"></a><span data-ttu-id="8d0bb-104">Get Started on Azure Dev Spaces with Node.js</span><span class="sxs-lookup"><span data-stu-id="8d0bb-104">Get Started on Azure Dev Spaces with Node.js</span></span>

[!INCLUDE [](includes/learning-objectives.md)]

[!INCLUDE [](includes/see-troubleshooting.md)]

<span data-ttu-id="8d0bb-105">You're now ready to create a Kubernetes-based development environment in Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-105">You're now ready to create a Kubernetes-based development environment in Azure.</span></span>

[!INCLUDE [](includes/portal-aks-cluster.md)]

## <a name="install-the-azure-cli"></a><span data-ttu-id="8d0bb-106">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8d0bb-106">Install the Azure CLI</span></span>
<span data-ttu-id="8d0bb-107">Azure Dev Spaces requires minimal local machine setup.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-107">Azure Dev Spaces requires minimal local machine setup.</span></span> <span data-ttu-id="8d0bb-108">Most of your dev space's configuration gets stored in the cloud, and is shareable with other users.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-108">Most of your dev space's configuration gets stored in the cloud, and is shareable with other users.</span></span> <span data-ttu-id="8d0bb-109">Your local machine can run Windows, Mac, or Linux.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-109">Your local machine can run Windows, Mac, or Linux.</span></span> <span data-ttu-id="8d0bb-110">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-110">For Linux, the following distributions are supported: Ubuntu (18.04, 16.04, and 14.04), Debian 8 and 9, RHEL 7, Fedora 26+, CentOS 7, openSUSE 42.2, and SLES 12.</span></span>

<span data-ttu-id="8d0bb-111">Start by downloading and running the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="8d0bb-111">Start by downloading and running the [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8d0bb-112">If you already have the Azure CLI installed, make sure you are using version 2.0.43 or higher.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-112">If you already have the Azure CLI installed, make sure you are using version 2.0.43 or higher.</span></span>

[!INCLUDE [](includes/sign-into-azure.md)]

[!INCLUDE [](includes/use-dev-spaces.md)]

[!INCLUDE [](includes/install-vscode-extension.md)]

<span data-ttu-id="8d0bb-113">While you're waiting for the cluster to be create, you can start writing code.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-113">While you're waiting for the cluster to be create, you can start writing code.</span></span>

## <a name="create-a-nodejs-container-in-kubernetes"></a><span data-ttu-id="8d0bb-114">Create a Node.js container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8d0bb-114">Create a Node.js container in Kubernetes</span></span>

<span data-ttu-id="8d0bb-115">In this section, you'll create a Node.js web app and get it running in a container in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-115">In this section, you'll create a Node.js web app and get it running in a container in Kubernetes.</span></span>

### <a name="create-a-nodejs-web-app"></a><span data-ttu-id="8d0bb-116">Create a Node.js Web App</span><span class="sxs-lookup"><span data-stu-id="8d0bb-116">Create a Node.js Web App</span></span>
<span data-ttu-id="8d0bb-117">Download code from GitHub by navigating to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository to your local environment.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-117">Download code from GitHub by navigating to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository to your local environment.</span></span> <span data-ttu-id="8d0bb-118">The code for this guide is in `samples/nodejs/getting-started/webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-118">The code for this guide is in `samples/nodejs/getting-started/webfrontend`.</span></span>

[!INCLUDE [](includes/azds-prep.md)]

[!INCLUDE [](includes/build-run-k8s-cli.md)]

### <a name="update-a-content-file"></a><span data-ttu-id="8d0bb-119">Update a content file</span><span class="sxs-lookup"><span data-stu-id="8d0bb-119">Update a content file</span></span>
<span data-ttu-id="8d0bb-120">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-120">Azure Dev Spaces isn't just about getting code running in Kubernetes - it's about enabling you to quickly and iteratively see your code changes take effect in a Kubernetes environment in the cloud.</span></span>

1. <span data-ttu-id="8d0bb-121">Locate the file `./public/index.html` and make an edit to the HTML.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-121">Locate the file `./public/index.html` and make an edit to the HTML.</span></span> <span data-ttu-id="8d0bb-122">For example, change the page's background color to a shade of blue:</span><span class="sxs-lookup"><span data-stu-id="8d0bb-122">For example, change the page's background color to a shade of blue:</span></span>

    ```html
    <body style="background-color: #95B9C7; margin-left:10px; margin-right:10px;">
    ```

2. <span data-ttu-id="8d0bb-123">Save the file.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-123">Save the file.</span></span> <span data-ttu-id="8d0bb-124">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-124">Moments later, in the Terminal window you'll see a message saying a file in the running container was updated.</span></span>
1. <span data-ttu-id="8d0bb-125">Go to your browser and refresh the page.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-125">Go to your browser and refresh the page.</span></span> <span data-ttu-id="8d0bb-126">You should see your color update.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-126">You should see your color update.</span></span>

<span data-ttu-id="8d0bb-127">What happened?</span><span class="sxs-lookup"><span data-stu-id="8d0bb-127">What happened?</span></span> <span data-ttu-id="8d0bb-128">Edits to content files, like HTML and CSS, don't require the Node.js process to restart, so an active `azds up` command will automatically sync any modified content files directly into the running container in Azure, thereby providing a fast way to see your content edits.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-128">Edits to content files, like HTML and CSS, don't require the Node.js process to restart, so an active `azds up` command will automatically sync any modified content files directly into the running container in Azure, thereby providing a fast way to see your content edits.</span></span>

### <a name="test-from-a-mobile-device"></a><span data-ttu-id="8d0bb-129">Test from a mobile device</span><span class="sxs-lookup"><span data-stu-id="8d0bb-129">Test from a mobile device</span></span>
<span data-ttu-id="8d0bb-130">Open the web app on a mobile device using the public URL for webfrontend.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-130">Open the web app on a mobile device using the public URL for webfrontend.</span></span> <span data-ttu-id="8d0bb-131">You may want to copy and send the URL from your desktop to your device to save you from entering the long address.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-131">You may want to copy and send the URL from your desktop to your device to save you from entering the long address.</span></span> <span data-ttu-id="8d0bb-132">When the web app loads in your mobile device, you will notice that the UI does not display properly on a small device.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-132">When the web app loads in your mobile device, you will notice that the UI does not display properly on a small device.</span></span>

<span data-ttu-id="8d0bb-133">To fix this, you'll add a `viewport` meta tag:</span><span class="sxs-lookup"><span data-stu-id="8d0bb-133">To fix this, you'll add a `viewport` meta tag:</span></span>
1. <span data-ttu-id="8d0bb-134">Open the file `./public/index.html`</span><span class="sxs-lookup"><span data-stu-id="8d0bb-134">Open the file `./public/index.html`</span></span>
1. <span data-ttu-id="8d0bb-135">Add a `viewport` meta tag in the existing `head` element:</span><span class="sxs-lookup"><span data-stu-id="8d0bb-135">Add a `viewport` meta tag in the existing `head` element:</span></span>

    ```html
    <head>
        <!-- Add this line -->
        <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    ```

1. <span data-ttu-id="8d0bb-136">Save the file.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-136">Save the file.</span></span>
1. <span data-ttu-id="8d0bb-137">Refresh your device's browser.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-137">Refresh your device's browser.</span></span> <span data-ttu-id="8d0bb-138">You should now see the web app rendered correctly.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-138">You should now see the web app rendered correctly.</span></span> 

<span data-ttu-id="8d0bb-139">This is an example of how some problems just aren't found until you test on the devices where an app is meant to be used.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-139">This is an example of how some problems just aren't found until you test on the devices where an app is meant to be used.</span></span> <span data-ttu-id="8d0bb-140">With Azure Dev Spaces, you can rapidly iterate on your code and validate any changes on target devices.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-140">With Azure Dev Spaces, you can rapidly iterate on your code and validate any changes on target devices.</span></span>

### <a name="update-a-code-file"></a><span data-ttu-id="8d0bb-141">Update a code file</span><span class="sxs-lookup"><span data-stu-id="8d0bb-141">Update a code file</span></span>
<span data-ttu-id="8d0bb-142">Updating server-side code files requires a little more work, because a Node.js app needs to restart.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-142">Updating server-side code files requires a little more work, because a Node.js app needs to restart.</span></span>

1. <span data-ttu-id="8d0bb-143">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span><span class="sxs-lookup"><span data-stu-id="8d0bb-143">In the terminal window, press `Ctrl+C` (to stop `azds up`).</span></span>
1. <span data-ttu-id="8d0bb-144">Open the code file named `server.js`, and edit service's hello message:</span><span class="sxs-lookup"><span data-stu-id="8d0bb-144">Open the code file named `server.js`, and edit service's hello message:</span></span> 

    ```javascript
    res.send('Hello from webfrontend running in Azure!');
    ```

3. <span data-ttu-id="8d0bb-145">Save the file.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-145">Save the file.</span></span>
1. <span data-ttu-id="8d0bb-146">Run  `azds up` in the terminal window.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-146">Run  `azds up` in the terminal window.</span></span> 

<span data-ttu-id="8d0bb-147">This rebuilds the container image and redeploys the Helm chart.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-147">This rebuilds the container image and redeploys the Helm chart.</span></span> <span data-ttu-id="8d0bb-148">Reload the browser page to see your code changes take effect.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-148">Reload the browser page to see your code changes take effect.</span></span>

<span data-ttu-id="8d0bb-149">But there is an even *faster method* for developing code, which you'll explore in the next section.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-149">But there is an even *faster method* for developing code, which you'll explore in the next section.</span></span> 

## <a name="debug-a-container-in-kubernetes"></a><span data-ttu-id="8d0bb-150">Debug a container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8d0bb-150">Debug a container in Kubernetes</span></span>

[!INCLUDE [](includes/debug-intro.md)]

[!INCLUDE [](includes/init-debug-assets-vscode.md)]

### <a name="select-the-azds-debug-configuration"></a><span data-ttu-id="8d0bb-151">Select the AZDS debug configuration</span><span class="sxs-lookup"><span data-stu-id="8d0bb-151">Select the AZDS debug configuration</span></span>
1. <span data-ttu-id="8d0bb-152">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-152">To open the Debug view, click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span>
1. <span data-ttu-id="8d0bb-153">Select **Launch Program (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-153">Select **Launch Program (AZDS)** as the active debug configuration.</span></span>

![](media/get-started-node/debug-configuration-nodejs2.png)

> [!Note]
> <span data-ttu-id="8d0bb-154">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have [installed the VS Code extension for Azure Dev Spaces](get-started-nodejs.md#get-kubernetes-debugging-for-vs-code).</span><span class="sxs-lookup"><span data-stu-id="8d0bb-154">If you don't see any Azure Dev Spaces commands in the Command Palette, ensure you have [installed the VS Code extension for Azure Dev Spaces](get-started-nodejs.md#get-kubernetes-debugging-for-vs-code).</span></span>

### <a name="debug-the-container-in-kubernetes"></a><span data-ttu-id="8d0bb-155">Debug the container in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="8d0bb-155">Debug the container in Kubernetes</span></span>
<span data-ttu-id="8d0bb-156">Hit **F5** to debug your code in Kubernetes!</span><span class="sxs-lookup"><span data-stu-id="8d0bb-156">Hit **F5** to debug your code in Kubernetes!</span></span>

<span data-ttu-id="8d0bb-157">Similar to the `up` command, code is synced to the development environment when you start debugging, and a container is built and deployed to Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-157">Similar to the `up` command, code is synced to the development environment when you start debugging, and a container is built and deployed to Kubernetes.</span></span> <span data-ttu-id="8d0bb-158">This time, the debugger is attached to the remote container.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-158">This time, the debugger is attached to the remote container.</span></span>

[!INCLUDE [](includes/tip-vscode-status-bar-url.md)]

<span data-ttu-id="8d0bb-159">Set a breakpoint in a server-side code file, for example within the `app.get('/api'...` in  `server.js`.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-159">Set a breakpoint in a server-side code file, for example within the `app.get('/api'...` in  `server.js`.</span></span> <span data-ttu-id="8d0bb-160">Refresh the browser page, or press the 'Say It Again' button, and you should hit the breakpoint and be able to step through code.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-160">Refresh the browser page, or press the 'Say It Again' button, and you should hit the breakpoint and be able to step through code.</span></span>

<span data-ttu-id="8d0bb-161">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-161">You have full access to debug information just like you would if the code was executing locally, such as the call stack, local variables, exception information, etc.</span></span>

### <a name="edit-code-and-refresh-the-debug-session"></a><span data-ttu-id="8d0bb-162">Edit code and refresh the debug session</span><span class="sxs-lookup"><span data-stu-id="8d0bb-162">Edit code and refresh the debug session</span></span>
<span data-ttu-id="8d0bb-163">With the debugger active, make a code edit; for example, modify the hello message again:</span><span class="sxs-lookup"><span data-stu-id="8d0bb-163">With the debugger active, make a code edit; for example, modify the hello message again:</span></span>

```javascript
app.get('/api', function (req, res) {
    res.send('**** Hello from webfrontend running in Azure! ****');
});
```

<span data-ttu-id="8d0bb-164">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-164">Save the file, and in the **Debug actions pane**, click the **Refresh** button.</span></span> 

![](media/get-started-node/debug-action-refresh-nodejs.png)

<span data-ttu-id="8d0bb-165">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will restart the Node.js process in between debug sessions to provide a faster edit/debug loop.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-165">Instead of rebuilding and redeploying a new container image each time code edits are made, which will often take considerable time, Azure Dev Spaces will restart the Node.js process in between debug sessions to provide a faster edit/debug loop.</span></span>

<span data-ttu-id="8d0bb-166">Refresh the web app in the browser, or press the *Say It Again* button.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-166">Refresh the web app in the browser, or press the *Say It Again* button.</span></span> <span data-ttu-id="8d0bb-167">You should see your custom message appear in the UI.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-167">You should see your custom message appear in the UI.</span></span>

### <a name="use-nodemon-to-develop-even-faster"></a><span data-ttu-id="8d0bb-168">Use NodeMon to develop even faster</span><span class="sxs-lookup"><span data-stu-id="8d0bb-168">Use NodeMon to develop even faster</span></span>
<span data-ttu-id="8d0bb-169">*Nodemon* is a popular tool that Node.js developers use for rapid development.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-169">*Nodemon* is a popular tool that Node.js developers use for rapid development.</span></span> <span data-ttu-id="8d0bb-170">Instead of manually restarting the Node process each time a server-side code edit is made, developers will often configure their Node project to have *nodemon* monitor file changes and automatically restart the server process.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-170">Instead of manually restarting the Node process each time a server-side code edit is made, developers will often configure their Node project to have *nodemon* monitor file changes and automatically restart the server process.</span></span> <span data-ttu-id="8d0bb-171">In this style of working, the developer just refreshes their browser after making a code edit.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-171">In this style of working, the developer just refreshes their browser after making a code edit.</span></span>

<span data-ttu-id="8d0bb-172">With Azure Dev Spaces, you can use many of the same development workflows you use when developing locally.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-172">With Azure Dev Spaces, you can use many of the same development workflows you use when developing locally.</span></span> <span data-ttu-id="8d0bb-173">To illustrate this, the sample `webfrontend` project was configured to use *nodemon* (it is configured as a dev dependency in `package.json`).</span><span class="sxs-lookup"><span data-stu-id="8d0bb-173">To illustrate this, the sample `webfrontend` project was configured to use *nodemon* (it is configured as a dev dependency in `package.json`).</span></span>

<span data-ttu-id="8d0bb-174">Try the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d0bb-174">Try the following steps:</span></span>
1. <span data-ttu-id="8d0bb-175">Stop the VS Code debugger.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-175">Stop the VS Code debugger.</span></span>
1. <span data-ttu-id="8d0bb-176">Click on the Debug icon in the **Activity Bar** on the side of VS Code.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-176">Click on the Debug icon in the **Activity Bar** on the side of VS Code.</span></span> 
1. <span data-ttu-id="8d0bb-177">Select **Attach (AZDS)** as the active debug configuration.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-177">Select **Attach (AZDS)** as the active debug configuration.</span></span>
1. <span data-ttu-id="8d0bb-178">Hit F5.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-178">Hit F5.</span></span>

<span data-ttu-id="8d0bb-179">In this configuration, the container is configured to start *nodemon*.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-179">In this configuration, the container is configured to start *nodemon*.</span></span> <span data-ttu-id="8d0bb-180">When server code edits are made, *nodemon* automatically restarts the Node process, just like it does when you develop locally.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-180">When server code edits are made, *nodemon* automatically restarts the Node process, just like it does when you develop locally.</span></span> 
1. <span data-ttu-id="8d0bb-181">Edit the hello message again in `server.js`, and save the file.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-181">Edit the hello message again in `server.js`, and save the file.</span></span>
1. <span data-ttu-id="8d0bb-182">Refresh the browser, or click the *Say It Again* button, to see your changes take effect!</span><span class="sxs-lookup"><span data-stu-id="8d0bb-182">Refresh the browser, or click the *Say It Again* button, to see your changes take effect!</span></span>

<span data-ttu-id="8d0bb-183">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span><span class="sxs-lookup"><span data-stu-id="8d0bb-183">**Now you have a method for rapidly iterating on code and debugging directly in Kubernetes!**</span></span> <span data-ttu-id="8d0bb-184">Next, you'll see how you can create and call a second container.</span><span class="sxs-lookup"><span data-stu-id="8d0bb-184">Next, you'll see how you can create and call a second container.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d0bb-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d0bb-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d0bb-186">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="8d0bb-186">Learn about team development</span></span>](team-development-nodejs.md)

