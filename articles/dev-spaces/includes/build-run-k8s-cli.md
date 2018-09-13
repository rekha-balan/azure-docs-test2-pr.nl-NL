---
title: include file
description: include file
ms.custom: include file
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: include
manager: douge
ms.openlocfilehash: b18cfce173da562aa7cffa48f336ff623c868f21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45181302"
---
## <a name="build-and-run-code-in-kubernetes"></a><span data-ttu-id="660f1-103">Build and run code in Kubernetes</span><span class="sxs-lookup"><span data-stu-id="660f1-103">Build and run code in Kubernetes</span></span>
<span data-ttu-id="660f1-104">Let's run our code!</span><span class="sxs-lookup"><span data-stu-id="660f1-104">Let's run our code!</span></span> <span data-ttu-id="660f1-105">In the terminal window, run this command from the **root code folder**, webfrontend:</span><span class="sxs-lookup"><span data-stu-id="660f1-105">In the terminal window, run this command from the **root code folder**, webfrontend:</span></span>

```cmd
azds up
```

<span data-ttu-id="660f1-106">Keep an eye on the command's output, you'll notice several things as it progresses:</span><span class="sxs-lookup"><span data-stu-id="660f1-106">Keep an eye on the command's output, you'll notice several things as it progresses:</span></span>
- <span data-ttu-id="660f1-107">Source code is synced to the dev space in Azure.</span><span class="sxs-lookup"><span data-stu-id="660f1-107">Source code is synced to the dev space in Azure.</span></span>
- <span data-ttu-id="660f1-108">A container image is built in Azure, as specified by the Docker assets in your code folder.</span><span class="sxs-lookup"><span data-stu-id="660f1-108">A container image is built in Azure, as specified by the Docker assets in your code folder.</span></span>
- <span data-ttu-id="660f1-109">Kubernetes objects are created that utilize the container image as specified by the Helm chart in your code folder.</span><span class="sxs-lookup"><span data-stu-id="660f1-109">Kubernetes objects are created that utilize the container image as specified by the Helm chart in your code folder.</span></span>
- <span data-ttu-id="660f1-110">Information about the container's endpoint(s) is displayed.</span><span class="sxs-lookup"><span data-stu-id="660f1-110">Information about the container's endpoint(s) is displayed.</span></span> <span data-ttu-id="660f1-111">In our case, we're expecting a public HTTP URL.</span><span class="sxs-lookup"><span data-stu-id="660f1-111">In our case, we're expecting a public HTTP URL.</span></span>
- <span data-ttu-id="660f1-112">Assuming the above stages complete successfully, you should begin to see `stdout` (and `stderr`) output as the container starts up.</span><span class="sxs-lookup"><span data-stu-id="660f1-112">Assuming the above stages complete successfully, you should begin to see `stdout` (and `stderr`) output as the container starts up.</span></span>

> [!Note]
> <span data-ttu-id="660f1-113">These steps will take longer the first time the `up` command is run, but subsequent runs should be quicker.</span><span class="sxs-lookup"><span data-stu-id="660f1-113">These steps will take longer the first time the `up` command is run, but subsequent runs should be quicker.</span></span>

### <a name="test-the-web-app"></a><span data-ttu-id="660f1-114">Test the web app</span><span class="sxs-lookup"><span data-stu-id="660f1-114">Test the web app</span></span>
<span data-ttu-id="660f1-115">Scan the console output for information about the public URL that was created by the `up` command.</span><span class="sxs-lookup"><span data-stu-id="660f1-115">Scan the console output for information about the public URL that was created by the `up` command.</span></span> <span data-ttu-id="660f1-116">It will be in the form:</span><span class="sxs-lookup"><span data-stu-id="660f1-116">It will be in the form:</span></span> 

`Service 'webfrontend' port 'http' is available at <url>` 

<span data-ttu-id="660f1-117">Open this URL in a browser window, and you should see the web app load.</span><span class="sxs-lookup"><span data-stu-id="660f1-117">Open this URL in a browser window, and you should see the web app load.</span></span> <span data-ttu-id="660f1-118">As the container executes, `stdout` and `stderr` output is streamed to the terminal window.</span><span class="sxs-lookup"><span data-stu-id="660f1-118">As the container executes, `stdout` and `stderr` output is streamed to the terminal window.</span></span>

> [!Note]
> <span data-ttu-id="660f1-119">On first run, it can take several minutes for public DNS to be ready.</span><span class="sxs-lookup"><span data-stu-id="660f1-119">On first run, it can take several minutes for public DNS to be ready.</span></span> <span data-ttu-id="660f1-120">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span><span class="sxs-lookup"><span data-stu-id="660f1-120">If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output.</span></span> <span data-ttu-id="660f1-121">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span><span class="sxs-lookup"><span data-stu-id="660f1-121">If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS.</span></span> <span data-ttu-id="660f1-122">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span><span class="sxs-lookup"><span data-stu-id="660f1-122">For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure.</span></span> <span data-ttu-id="660f1-123">You can come back and try the public URL later when the DNS record is ready.</span><span class="sxs-lookup"><span data-stu-id="660f1-123">You can come back and try the public URL later when the DNS record is ready.</span></span>
