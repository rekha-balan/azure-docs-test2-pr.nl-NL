---
title: Team development with Azure Dev Spaces using .NET Core and VS Code| Microsoft Docs
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
ms.openlocfilehash: 602e2a691dfa150c2e8332cb6dca070dbdd57901
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869318"
---
# <a name="team-development-with-azure-dev-spaces"></a><span data-ttu-id="741b7-104">Team Development with Azure Dev Spaces</span><span class="sxs-lookup"><span data-stu-id="741b7-104">Team Development with Azure Dev Spaces</span></span>

<span data-ttu-id="741b7-105">In this tutorial, you'll learn how to use multiple dev spaces to work simultaneously in different development environments, keeping separate work in separate dev spaces in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="741b7-105">In this tutorial, you'll learn how to use multiple dev spaces to work simultaneously in different development environments, keeping separate work in separate dev spaces in the same cluster.</span></span>

## <a name="call-a-service-running-in-a-separate-container"></a><span data-ttu-id="741b7-106">Call a service running in a separate container</span><span class="sxs-lookup"><span data-stu-id="741b7-106">Call a service running in a separate container</span></span>

<span data-ttu-id="741b7-107">In this section, you create a second service, `mywebapi`, and have `webfrontend` call it.</span><span class="sxs-lookup"><span data-stu-id="741b7-107">In this section, you create a second service, `mywebapi`, and have `webfrontend` call it.</span></span> <span data-ttu-id="741b7-108">Each service will run in separate containers.</span><span class="sxs-lookup"><span data-stu-id="741b7-108">Each service will run in separate containers.</span></span> <span data-ttu-id="741b7-109">You'll then debug across both containers.</span><span class="sxs-lookup"><span data-stu-id="741b7-109">You'll then debug across both containers.</span></span>

![Multiple containers](media/common/multi-container.png)

### <a name="download-sample-code-for-mywebapi"></a><span data-ttu-id="741b7-111">Download sample code for *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="741b7-111">Download sample code for *mywebapi*</span></span>
<span data-ttu-id="741b7-112">For the sake of time, let's download sample code from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="741b7-112">For the sake of time, let's download sample code from a GitHub repository.</span></span> <span data-ttu-id="741b7-113">Go to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="741b7-113">Go to https://github.com/Azure/dev-spaces and select **Clone or Download** to download the GitHub repository.</span></span> <span data-ttu-id="741b7-114">The code for this section is in `samples/dotnetcore/getting-started/mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="741b7-114">The code for this section is in `samples/dotnetcore/getting-started/mywebapi`.</span></span>

### <a name="run-mywebapi"></a><span data-ttu-id="741b7-115">Run *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="741b7-115">Run *mywebapi*</span></span>
1. <span data-ttu-id="741b7-116">Open the folder `mywebapi` in a *separate VS Code window*.</span><span class="sxs-lookup"><span data-stu-id="741b7-116">Open the folder `mywebapi` in a *separate VS Code window*.</span></span>
1. <span data-ttu-id="741b7-117">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span><span class="sxs-lookup"><span data-stu-id="741b7-117">Open the **Command Palette** (using the **View | Command Palette** menu), and use auto-complete to type and select this command: `Azure Dev Spaces: Prepare configuration files for Azure Dev Spaces`.</span></span> <span data-ttu-id="741b7-118">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span><span class="sxs-lookup"><span data-stu-id="741b7-118">This command is not to be confused with the `azds prep` command, which configures the project for deployment.</span></span>
1. <span data-ttu-id="741b7-119">Hit F5, and wait for the service to build and deploy.</span><span class="sxs-lookup"><span data-stu-id="741b7-119">Hit F5, and wait for the service to build and deploy.</span></span> <span data-ttu-id="741b7-120">You'll know it's ready when the VS Code debug bar appears.</span><span class="sxs-lookup"><span data-stu-id="741b7-120">You'll know it's ready when the VS Code debug bar appears.</span></span>
1. <span data-ttu-id="741b7-121">The endpoint URL will look something like http://localhost:\<portnumber\>.</span><span class="sxs-lookup"><span data-stu-id="741b7-121">The endpoint URL will look something like http://localhost:\<portnumber\>.</span></span> <span data-ttu-id="741b7-122">**Tip: The VS Code status bar will display a clickable URL.**</span><span class="sxs-lookup"><span data-stu-id="741b7-122">**Tip: The VS Code status bar will display a clickable URL.**</span></span> <span data-ttu-id="741b7-123">It might seem like the container is running locally, but actually it is running in our dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="741b7-123">It might seem like the container is running locally, but actually it is running in our dev space in Azure.</span></span> <span data-ttu-id="741b7-124">The reason for the localhost address is because `mywebapi` has not defined any public endpoints and can only be accessed from within the Kubernetes instance.</span><span class="sxs-lookup"><span data-stu-id="741b7-124">The reason for the localhost address is because `mywebapi` has not defined any public endpoints and can only be accessed from within the Kubernetes instance.</span></span> <span data-ttu-id="741b7-125">For your convenience, and to facilitate interacting with the private service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="741b7-125">For your convenience, and to facilitate interacting with the private service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span>
1. <span data-ttu-id="741b7-126">When `mywebapi` is ready, open your browser to the localhost address.</span><span class="sxs-lookup"><span data-stu-id="741b7-126">When `mywebapi` is ready, open your browser to the localhost address.</span></span> <span data-ttu-id="741b7-127">Append `/api/values` to the URL to invoke the default GET API for the `ValuesController`.</span><span class="sxs-lookup"><span data-stu-id="741b7-127">Append `/api/values` to the URL to invoke the default GET API for the `ValuesController`.</span></span> 
1. <span data-ttu-id="741b7-128">If all the steps were successful, you should be able to see a response from the `mywebapi` service.</span><span class="sxs-lookup"><span data-stu-id="741b7-128">If all the steps were successful, you should be able to see a response from the `mywebapi` service.</span></span>

### <a name="make-a-request-from-webfrontend-to-mywebapi"></a><span data-ttu-id="741b7-129">Make a request from *webfrontend* to *mywebapi*</span><span class="sxs-lookup"><span data-stu-id="741b7-129">Make a request from *webfrontend* to *mywebapi*</span></span>
<span data-ttu-id="741b7-130">Let's now write code in `webfrontend` that makes a request to `mywebapi`.</span><span class="sxs-lookup"><span data-stu-id="741b7-130">Let's now write code in `webfrontend` that makes a request to `mywebapi`.</span></span>
1. <span data-ttu-id="741b7-131">Switch to the VS Code window for `webfrontend`.</span><span class="sxs-lookup"><span data-stu-id="741b7-131">Switch to the VS Code window for `webfrontend`.</span></span>
1. <span data-ttu-id="741b7-132">*Replace* the code for the About method:</span><span class="sxs-lookup"><span data-stu-id="741b7-132">*Replace* the code for the About method:</span></span>

    ```csharp
    public async Task<IActionResult> About()
    {
        ViewData["Message"] = "Hello from webfrontend";
        
        using (var client = new System.Net.Http.HttpClient())
            {
                // Call *mywebapi*, and display its response in the page
                var request = new System.Net.Http.HttpRequestMessage();
                request.RequestUri = new Uri("http://mywebapi/api/values/1");
                if (this.Request.Headers.ContainsKey("azds-route-as"))
                {
                    // Propagate the dev space routing header
                    request.Headers.Add("azds-route-as", this.Request.Headers["azds-route-as"] as IEnumerable<string>);
                }
                var response = await client.SendAsync(request);
                ViewData["Message"] += " and " + await response.Content.ReadAsStringAsync();
            }

        return View();
    }
    ```

<span data-ttu-id="741b7-133">The preceding code example forwards the `azds-route-as` header from the incoming request to the outgoing request.</span><span class="sxs-lookup"><span data-stu-id="741b7-133">The preceding code example forwards the `azds-route-as` header from the incoming request to the outgoing request.</span></span> <span data-ttu-id="741b7-134">You'll see later how this helps teams with collaborative development.</span><span class="sxs-lookup"><span data-stu-id="741b7-134">You'll see later how this helps teams with collaborative development.</span></span>

### <a name="debug-across-multiple-services"></a><span data-ttu-id="741b7-135">Debug across multiple services</span><span class="sxs-lookup"><span data-stu-id="741b7-135">Debug across multiple services</span></span>
1. <span data-ttu-id="741b7-136">At this point, `mywebapi` should still be running with the debugger attached.</span><span class="sxs-lookup"><span data-stu-id="741b7-136">At this point, `mywebapi` should still be running with the debugger attached.</span></span> <span data-ttu-id="741b7-137">If it is not, hit F5 in the `mywebapi` project.</span><span class="sxs-lookup"><span data-stu-id="741b7-137">If it is not, hit F5 in the `mywebapi` project.</span></span>
1. <span data-ttu-id="741b7-138">Set a breakpoint in the `Get(int id)` method that handles `api/values/{id}` GET requests.</span><span class="sxs-lookup"><span data-stu-id="741b7-138">Set a breakpoint in the `Get(int id)` method that handles `api/values/{id}` GET requests.</span></span>
1. <span data-ttu-id="741b7-139">In the `webfrontend` project, set a breakpoint just before it sends a GET request to `mywebapi/api/values`.</span><span class="sxs-lookup"><span data-stu-id="741b7-139">In the `webfrontend` project, set a breakpoint just before it sends a GET request to `mywebapi/api/values`.</span></span>
1. <span data-ttu-id="741b7-140">Hit F5 in the `webfrontend` project.</span><span class="sxs-lookup"><span data-stu-id="741b7-140">Hit F5 in the `webfrontend` project.</span></span>
1. <span data-ttu-id="741b7-141">Invoke the web app, and step through code in both services.</span><span class="sxs-lookup"><span data-stu-id="741b7-141">Invoke the web app, and step through code in both services.</span></span>
1. <span data-ttu-id="741b7-142">In the web app, the About page will display a message concatenated by the two services: "Hello from webfrontend and Hello from mywebapi."</span><span class="sxs-lookup"><span data-stu-id="741b7-142">In the web app, the About page will display a message concatenated by the two services: "Hello from webfrontend and Hello from mywebapi."</span></span>


<span data-ttu-id="741b7-143">Well done!</span><span class="sxs-lookup"><span data-stu-id="741b7-143">Well done!</span></span> <span data-ttu-id="741b7-144">You now have a multi-container application where each container can be developed and deployed separately.</span><span class="sxs-lookup"><span data-stu-id="741b7-144">You now have a multi-container application where each container can be developed and deployed separately.</span></span>

## <a name="learn-about-team-development"></a><span data-ttu-id="741b7-145">Learn about team development</span><span class="sxs-lookup"><span data-stu-id="741b7-145">Learn about team development</span></span>

[!INCLUDE [](includes/team-development-1.md)]

<span data-ttu-id="741b7-146">Let's see it in action.</span><span class="sxs-lookup"><span data-stu-id="741b7-146">Let's see it in action.</span></span> <span data-ttu-id="741b7-147">Go to the VS Code window for `mywebapi` and make a code edit to the `string Get(int id)` method, for example:</span><span class="sxs-lookup"><span data-stu-id="741b7-147">Go to the VS Code window for `mywebapi` and make a code edit to the `string Get(int id)` method, for example:</span></span>

```csharp
[HttpGet("{id}")]
public string Get(int id)
{
    return "mywebapi now says something new";
}
```


[!INCLUDE [](includes/team-development-2.md)]

[!INCLUDE [](includes/well-done.md)]

[!INCLUDE [](includes/clean-up.md)]
