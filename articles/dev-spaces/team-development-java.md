---
title: Team development with Azure Dev Spaces using Java and VS Code| Microsoft Docs
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
ms.openlocfilehash: 1b3ab02c7214a40546c0fa6fdef16b4623a156e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871517"
---
# <a name="team-development-with-azure-dev-spaces"></a><span data-ttu-id="18284-104">Team Development with Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="18284-104">Team Development with Azure Dev Spaces</span></span>

<span data-ttu-id="18284-105">In this tutorial, you'll learn how to use multiple dev spaces to work simultaneously in different development environments, keeping separate work in separate dev spaces in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="18284-105">In this tutorial, you'll learn how to use multiple dev spaces to work simultaneously in different development environments, keeping separate work in separate dev spaces in the same cluster.</span></span>

## <a name="call-a-service-running-in-a-separate-container"></a><span data-ttu-id="18284-106">Call a service running in a separate container</span><span class="sxs-lookup"><span data-stu-id="18284-106">Call a service running in a separate container</span></span>

<span data-ttu-id="18284-107">In this section, you create a second service, `mywebapi`, and have `webfrontend` call it.</span><span class="sxs-lookup"><span data-stu-id="18284-107">In this section, you create a second service, `mywebapi`, and have `webfrontend` call it.</span></span> <span data-ttu-id="18284-108">Each service will run in separate containers.</span><span class="sxs-lookup"><span data-stu-id="18284-108">Each service will run in separate containers.</span></span> <span data-ttu-id="18284-109">You'll then debug across both containers.</span><span class="sxs-lookup"><span data-stu-id="18284-109">You'll then debug across both containers.</span></span>

![Multiple containers](media/common/multi-container.png)

### <a name="download-sample-code-for-mywebapi"></a><span data-ttu-id="18284-111">Download sample code for *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="18284-111">Download sample code for *mywebapi*</span></span>
<span data-ttu-id="18284-112">For the sake of time, let's download sample code from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="18284-112">For the sake of time, let's download sample code from a GitHub repository.</span></span> <span data-ttu-id="18284-113">Go to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="18284-113">Go to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository.</span></span> <span data-ttu-id="18284-114">The code for this section is in `samples/java/getting-started/mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="18284-114">The code for this section is in `samples/java/getting-started/mywebapi`.</span></span>

### <a name="run-mywebapi"></a><span data-ttu-id="18284-115">Run *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="18284-115">Run *mywebapi*</span></span>
1. <span data-ttu-id="18284-116">Open the folder `mywebapi` in a *separate VS Code window*.</span><span class="sxs-lookup"><span data-stu-id="18284-116">Open the folder `mywebapi` in a *separate VS Code window*.</span></span>
1. <span data-ttu-id="18284-117">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span><span class="sxs-lookup"><span data-stu-id="18284-117">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span></span>
1. <span data-ttu-id="18284-118">Hit F5, and wait for the service to build and deploy.</span><span class="sxs-lookup"><span data-stu-id="18284-118">Hit F5, and wait for the service to build and deploy.</span></span> <span data-ttu-id="18284-119">You'll know it's ready when the VS Code debug bar appears.</span><span class="sxs-lookup"><span data-stu-id="18284-119">You'll know it's ready when the VS Code debug bar appears.</span></span>
1. <span data-ttu-id="18284-120">The endpoint URL will look something like http://localhost:\<portnumber\>.</span><span class="sxs-lookup"><span data-stu-id="18284-120">The endpoint URL will look something like http://localhost:\<portnumber\>.</span></span> <span data-ttu-id="18284-121">**Tip: The VS Code status bar will display a clickable URL.**</span><span class="sxs-lookup"><span data-stu-id="18284-121">**Tip: The VS Code status bar will display a clickable URL.**</span></span> <span data-ttu-id="18284-122">It might seem like the container is running locally, but actually it is running in our dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="18284-122">It might seem like the container is running locally, but actually it is running in our dev space in Azure.</span></span> <span data-ttu-id="18284-123">The reason for the localhost address is because `mywebapi` has not defined any public endpoints and can only be accessed from within the Kubernetes instance.</span><span class="sxs-lookup"><span data-stu-id="18284-123">The reason for the localhost address is because `mywebapi` has not defined any public endpoints and can only be accessed from within the Kubernetes instance.</span></span> <span data-ttu-id="18284-124">For your convenience, and to facilitate interacting with the private service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="18284-124">For your convenience, and to facilitate interacting with the private service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span>
1. <span data-ttu-id="18284-125">When `mywebapi` is ready, open your browser to the localhost address.</span><span class="sxs-lookup"><span data-stu-id="18284-125">When `mywebapi` is ready, open your browser to the localhost address.</span></span>
1. <span data-ttu-id="18284-126">If all the steps were successful, you should be able to see a response from the `mywebapi` service.</span><span class="sxs-lookup"><span data-stu-id="18284-126">If all the steps were successful, you should be able to see a response from the `mywebapi` service.</span></span>

### <a name="make-a-request-from-webfrontend-to-mywebapi"></a><span data-ttu-id="18284-127">Make a request from *webfrontend* to *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="18284-127">Make a request from *webfrontend* to *mywebapi*</span></span>
<span data-ttu-id="18284-128">Let's now write code in `webfrontend` that makes a request to `mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="18284-128">Let's now write code in `webfrontend` that makes a request to `mywebapi`.</span></span>
1. <span data-ttu-id="18284-129">Switch to the VS Code window for `webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="18284-129">Switch to the VS Code window for `webfrontend`.</span></span>
1. <span data-ttu-id="18284-130">*Add* the following `import` statements under the `package` statement:</span><span class="sxs-lookup"><span data-stu-id="18284-130">*Add* the following `import` statements under the `package` statement:</span></span>

   ```java
   import java.io.*;
   import java.net.*;
   ```
1. <span data-ttu-id="18284-131">*Replace* the code for the greeting method:</span><span class="sxs-lookup"><span data-stu-id="18284-131">*Replace* the code for the greeting method:</span></span>

    ```java
    @RequestMapping(value = "/greeting", produces = "text/plain")
    public String greeting(@RequestHeader(value = "azds-route-as", required = false) String azdsRouteAs) throws Exception {
        URLConnection conn = new URL("http://mywebapi/").openConnection();
        conn.setRequestProperty("azds-route-as", azdsRouteAs); // propagate dev space routing header
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream())))
        {
            return "Hello from webfrontend and " + reader.lines().reduce("\n", String::concat);
        }
    }
    ```

<span data-ttu-id="18284-132">The preceding code example forwards the `azds-route-as` header from the incoming request to the outgoing request.</span><span class="sxs-lookup"><span data-stu-id="18284-132">The preceding code example forwards the `azds-route-as` header from the incoming request to the outgoing request.</span></span> <span data-ttu-id="18284-133">You'll see later how this helps teams with collaborative development.</span><span class="sxs-lookup"><span data-stu-id="18284-133">You'll see later how this helps teams with collaborative development.</span></span>

### <a name="debug-across-multiple-services"></a><span data-ttu-id="18284-134">Debug across multiple services</span><span class="sxs-lookup"><span data-stu-id="18284-134">Debug across multiple services</span></span>
1. <span data-ttu-id="18284-135">At this point, `mywebapi` should still be running with the debugger attached.</span><span class="sxs-lookup"><span data-stu-id="18284-135">At this point, `mywebapi` should still be running with the debugger attached.</span></span> <span data-ttu-id="18284-136">If it is not, hit F5 in the `mywebapi` project.</span><span class="sxs-lookup"><span data-stu-id="18284-136">If it is not, hit F5 in the `mywebapi` project.</span></span>
1. <span data-ttu-id="18284-137">Set a breakpoint in the `index()` method of the `webapi` project.</span><span class="sxs-lookup"><span data-stu-id="18284-137">Set a breakpoint in the `index()` method of the `webapi` project.</span></span>
1. <span data-ttu-id="18284-138">In the `webfrontend` project, set a breakpoint just before it sends a GET request to `mywebapi`, on the line starting with `try`.</span><span class="sxs-lookup"><span data-stu-id="18284-138">In the `webfrontend` project, set a breakpoint just before it sends a GET request to `mywebapi`, on the line starting with `try`.</span></span>
1. <span data-ttu-id="18284-139">Hit F5 in the `webfrontend` project (or restart the debugger if currently running).</span><span class="sxs-lookup"><span data-stu-id="18284-139">Hit F5 in the `webfrontend` project (or restart the debugger if currently running).</span></span>
1. <span data-ttu-id="18284-140">Invoke the web app, and step through code in both services.</span><span class="sxs-lookup"><span data-stu-id="18284-140">Invoke the web app, and step through code in both services.</span></span>
1. <span data-ttu-id="18284-141">In the web app, the About page will display a message concatenated by the two services: "Hello from webfrontend and Hello from mywebapi."</span><span class="sxs-lookup"><span data-stu-id="18284-141">In the web app, the About page will display a message concatenated by the two services: "Hello from webfrontend and Hello from mywebapi."</span></span>

<span data-ttu-id="18284-142">Well done!</span><span class="sxs-lookup"><span data-stu-id="18284-142">Well done!</span></span> <span data-ttu-id="18284-143">You now have a multi-container application where each container can be developed and deployed separately.</span><span class="sxs-lookup"><span data-stu-id="18284-143">You now have a multi-container application where each container can be developed and deployed separately.</span></span>

## <a name="learn-about-team-development"></a><span data-ttu-id="18284-144">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="18284-144">Learn about team development</span></span>

[!INCLUDE[](includes/team-development-1.md)]

<span data-ttu-id="18284-145">Let's see it in action.</span><span class="sxs-lookup"><span data-stu-id="18284-145">Let's see it in action.</span></span> <span data-ttu-id="18284-146">Go to the VS Code window for `mywebapi` and make a code edit to the `String index()` method, for example:</span><span class="sxs-lookup"><span data-stu-id="18284-146">Go to the VS Code window for `mywebapi` and make a code edit to the `String index()` method, for example:</span></span>

```java
@RequestMapping(value = "/", produces = "text/plain")
public String index() {
    return "Hello from mywebapi says something new";
}
```

[!INCLUDE[](includes/team-development-2.md)]

[!INCLUDE[](includes/well-done.md)]

[!INCLUDE[](includes/clean-up.md)]
