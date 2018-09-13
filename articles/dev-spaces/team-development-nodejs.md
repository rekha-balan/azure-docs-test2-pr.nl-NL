---
title: Team development with Azure Dev Spaces with VS Code | Microsoft Docs
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
ms.openlocfilehash: b4c355c864f83bcd76c310fecb0f26dd3372e760
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870003"
---
# <a name="team-development-with-azure-dev-spaces"></a><span data-ttu-id="83569-104">Team development with Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="83569-104">Team development with Azure Dev Spaces</span></span>

<span data-ttu-id="83569-105">In this tutorial, you'll learn how to use multiple dev spaces to work simultaneously in different development environments, keeping separate work in separate dev spaces in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="83569-105">In this tutorial, you'll learn how to use multiple dev spaces to work simultaneously in different development environments, keeping separate work in separate dev spaces in the same cluster.</span></span>

## <a name="call-a-service-running-in-a-separate-container"></a><span data-ttu-id="83569-106">Call a service running in a separate container</span><span class="sxs-lookup"><span data-stu-id="83569-106">Call a service running in a separate container</span></span>

<span data-ttu-id="83569-107">In this section you're going to create a second service, `mywebapi`, and have `webfrontend` call it.</span><span class="sxs-lookup"><span data-stu-id="83569-107">In this section you're going to create a second service, `mywebapi`, and have `webfrontend` call it.</span></span> <span data-ttu-id="83569-108">Each service will run in separate containers.</span><span class="sxs-lookup"><span data-stu-id="83569-108">Each service will run in separate containers.</span></span> <span data-ttu-id="83569-109">You'll then debug across both containers.</span><span class="sxs-lookup"><span data-stu-id="83569-109">You'll then debug across both containers.</span></span>

![](media/common/multi-container.png)

### <a name="open-sample-code-for-mywebapi"></a><span data-ttu-id="83569-110">Open sample code for *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="83569-110">Open sample code for *mywebapi*</span></span>
<span data-ttu-id="83569-111">You should already have the sample code for `mywebapi` for this guide under a folder named `samples` (if not, go to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository.) The code for this section is in `samples/nodejs/getting-started/mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="83569-111">You should already have the sample code for `mywebapi` for this guide under a folder named `samples` (if not, go to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository.) The code for this section is in `samples/nodejs/getting-started/mywebapi`.</span></span>

### <a name="run-mywebapi"></a><span data-ttu-id="83569-112">Run *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="83569-112">Run *mywebapi*</span></span>
1. <span data-ttu-id="83569-113">Open the folder `mywebapi` in a *separate VS Code window*.</span><span class="sxs-lookup"><span data-stu-id="83569-113">Open the folder `mywebapi` in a *separate VS Code window*.</span></span>
1. <span data-ttu-id="83569-114">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span><span class="sxs-lookup"><span data-stu-id="83569-114">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span></span> <span data-ttu-id="83569-115">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span><span class="sxs-lookup"><span data-stu-id="83569-115">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span></span>
1. <span data-ttu-id="83569-116">Hit F5, and wait for the service to build and deploy.</span><span class="sxs-lookup"><span data-stu-id="83569-116">Hit F5, and wait for the service to build and deploy.</span></span> <span data-ttu-id="83569-117">You'll know it's ready when the VS Code debug bar appears.</span><span class="sxs-lookup"><span data-stu-id="83569-117">You'll know it's ready when the VS Code debug bar appears.</span></span>
1. <span data-ttu-id="83569-118">Take note of the endpoint URL, it will look something like http://localhost:\<portnumber\>.</span><span class="sxs-lookup"><span data-stu-id="83569-118">Take note of the endpoint URL, it will look something like http://localhost:\<portnumber\>.</span></span> <span data-ttu-id="83569-119">**Tip: The VS Code status bar will display a clickable URL.**</span><span class="sxs-lookup"><span data-stu-id="83569-119">**Tip: The VS Code status bar will display a clickable URL.**</span></span> <span data-ttu-id="83569-120">It may seem like the container is running locally, but actually it is running in your development environment in Azure.</span><span class="sxs-lookup"><span data-stu-id="83569-120">It may seem like the container is running locally, but actually it is running in your development environment in Azure.</span></span> <span data-ttu-id="83569-121">The reason for the localhost address is because `mywebapi` has not defined any public endpoints and can only be accessed from within the Kubernetes instance.</span><span class="sxs-lookup"><span data-stu-id="83569-121">The reason for the localhost address is because `mywebapi` has not defined any public endpoints and can only be accessed from within the Kubernetes instance.</span></span> <span data-ttu-id="83569-122">For your convenience, and to facilitate interacting with the private service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="83569-122">For your convenience, and to facilitate interacting with the private service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span>
1. <span data-ttu-id="83569-123">When `mywebapi` is ready, open your browser to the localhost address.</span><span class="sxs-lookup"><span data-stu-id="83569-123">When `mywebapi` is ready, open your browser to the localhost address.</span></span> <span data-ttu-id="83569-124">You should see a response from the `mywebapi` service ("Hello from mywebapi").</span><span class="sxs-lookup"><span data-stu-id="83569-124">You should see a response from the `mywebapi` service ("Hello from mywebapi").</span></span>


### <a name="make-a-request-from-webfrontend-to-mywebapi"></a><span data-ttu-id="83569-125">Make a request from *webfrontend* to *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="83569-125">Make a request from *webfrontend* to *mywebapi*</span></span>
<span data-ttu-id="83569-126">Let's now write code in `webfrontend` that makes a request to `mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="83569-126">Let's now write code in `webfrontend` that makes a request to `mywebapi`.</span></span>
1. <span data-ttu-id="83569-127">Switch to the VS Code window for `webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="83569-127">Switch to the VS Code window for `webfrontend`.</span></span>
1. <span data-ttu-id="83569-128">Add these lines of code at the top of `server.js`:</span><span class="sxs-lookup"><span data-stu-id="83569-128">Add these lines of code at the top of `server.js`:</span></span>
    ```javascript
    var request = require('request');
    ```

3. <span data-ttu-id="83569-129">*Replace* the code for the `/api` GET handler.</span><span class="sxs-lookup"><span data-stu-id="83569-129">*Replace* the code for the `/api` GET handler.</span></span> <span data-ttu-id="83569-130">When handling a request, it in turn makes a call to `mywebapi`, and then returns the results from both services.</span><span class="sxs-lookup"><span data-stu-id="83569-130">When handling a request, it in turn makes a call to `mywebapi`, and then returns the results from both services.</span></span>

    ```javascript
    app.get('/api', function (req, res) {
       request({
          uri: 'http://mywebapi',
          headers: {
             /* propagate the dev space routing header */
             'azds-route-as': req.headers['azds-route-as']
          }
       }, function (error, response, body) {
           res.send('Hello from webfrontend and ' + body);
       });
    });
    ```

<span data-ttu-id="83569-131">The preceding code example forwards the `azds-route-as` header from the incoming request to the outgoing request.</span><span class="sxs-lookup"><span data-stu-id="83569-131">The preceding code example forwards the `azds-route-as` header from the incoming request to the outgoing request.</span></span> <span data-ttu-id="83569-132">You'll see later how this helps teams with collaborative development.</span><span class="sxs-lookup"><span data-stu-id="83569-132">You'll see later how this helps teams with collaborative development.</span></span>

### <a name="debug-across-multiple-services"></a><span data-ttu-id="83569-133">Debug across multiple services</span><span class="sxs-lookup"><span data-stu-id="83569-133">Debug across multiple services</span></span>
1. <span data-ttu-id="83569-134">At this point, `mywebapi` should still be running with the debugger attached.</span><span class="sxs-lookup"><span data-stu-id="83569-134">At this point, `mywebapi` should still be running with the debugger attached.</span></span> <span data-ttu-id="83569-135">If it is not, hit F5 in the `mywebapi` project.</span><span class="sxs-lookup"><span data-stu-id="83569-135">If it is not, hit F5 in the `mywebapi` project.</span></span>
1. <span data-ttu-id="83569-136">Set a breakpoint in the default GET `/` handler.</span><span class="sxs-lookup"><span data-stu-id="83569-136">Set a breakpoint in the default GET `/` handler.</span></span>
1. <span data-ttu-id="83569-137">In the `webfrontend` project, set a breakpoint just before it sends a GET request to `http://mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="83569-137">In the `webfrontend` project, set a breakpoint just before it sends a GET request to `http://mywebapi`.</span></span>
1. <span data-ttu-id="83569-138">Hit F5 in the `webfrontend` project.</span><span class="sxs-lookup"><span data-stu-id="83569-138">Hit F5 in the `webfrontend` project.</span></span>
1. <span data-ttu-id="83569-139">Open the web app, and step through code in both services.</span><span class="sxs-lookup"><span data-stu-id="83569-139">Open the web app, and step through code in both services.</span></span> <span data-ttu-id="83569-140">The web app should display a message concatenated by the two services: "Hello from webfrontend and Hello from mywebapi."</span><span class="sxs-lookup"><span data-stu-id="83569-140">The web app should display a message concatenated by the two services: "Hello from webfrontend and Hello from mywebapi."</span></span>

<span data-ttu-id="83569-141">Well done!</span><span class="sxs-lookup"><span data-stu-id="83569-141">Well done!</span></span> <span data-ttu-id="83569-142">You now have a multi-container application where each container can be developed and deployed separately.</span><span class="sxs-lookup"><span data-stu-id="83569-142">You now have a multi-container application where each container can be developed and deployed separately.</span></span>

## <a name="learn-about-team-development"></a><span data-ttu-id="83569-143">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="83569-143">Learn about team development</span></span>

[!INCLUDE [](includes/team-development-1.md)]

<span data-ttu-id="83569-144">Now see it in action:</span><span class="sxs-lookup"><span data-stu-id="83569-144">Now see it in action:</span></span>
1. <span data-ttu-id="83569-145">Go to the VS Code window for `mywebapi` and make a code edit to the default GET `/` handler, for example:</span><span class="sxs-lookup"><span data-stu-id="83569-145">Go to the VS Code window for `mywebapi` and make a code edit to the default GET `/` handler, for example:</span></span>

    ```javascript
    app.get('/', function (req, res) {
        res.send('mywebapi now says something new');
    });
    ```

[!INCLUDE [](includes/team-development-2.md)]

[!INCLUDE [](includes/well-done.md)]

[!INCLUDE [](includes/clean-up.md)]




