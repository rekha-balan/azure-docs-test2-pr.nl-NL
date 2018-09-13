---
title: Push Docker image to private Azure registry | Microsoft Docs
description: Push and pull Docker images to a private container registry in Azure using the Docker CLI
services: container-registry
documentationcenter: ''
author: stevelas
manager: balans
editor: cristyg
tags: ''
keywords: ''
ms.assetid: 64fbe43f-fdde-4c17-a39a-d04f2d6d90a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2016
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 46be821275193ea9620e3f1959193a5c69105b78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555505"
---
# <a name="push-your-first-image-to-a-private-docker-container-registry-using-the-docker-cli"></a><span data-ttu-id="aa116-103">Push your first image to a private Docker container registry using the Docker CLI</span><span class="sxs-lookup"><span data-stu-id="aa116-103">Push your first image to a private Docker container registry using the Docker CLI</span></span>
<span data-ttu-id="aa116-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span><span class="sxs-lookup"><span data-stu-id="aa116-104">An Azure container registry stores and manages private [Docker](http://hub.docker.com) container images, similar to the way [Docker Hub](https://hub.docker.com/) stores public Docker images.</span></span> <span data-ttu-id="aa116-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span><span class="sxs-lookup"><span data-stu-id="aa116-105">You use the [Docker Command-Line Interface](https://docs.docker.com/engine/reference/commandline/cli/) (Docker CLI) for [login](https://docs.docker.com/engine/reference/commandline/login/), [push](https://docs.docker.com/engine/reference/commandline/push/), [pull](https://docs.docker.com/engine/reference/commandline/pull/), and other operations on your container registry.</span></span>

<span data-ttu-id="aa116-106">For more background and concepts, see [the overview](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="aa116-106">For more background and concepts, see [the overview](container-registry-intro.md)</span></span>



## <a name="prerequisites"></a><span data-ttu-id="aa116-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aa116-107">Prerequisites</span></span>
* <span data-ttu-id="aa116-108">**Azure container registry** - Create a container registry in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="aa116-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="aa116-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="aa116-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="aa116-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="aa116-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>

## <a name="log-in-to-a-registry"></a><span data-ttu-id="aa116-111">Log in to a registry</span><span class="sxs-lookup"><span data-stu-id="aa116-111">Log in to a registry</span></span>
<span data-ttu-id="aa116-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="aa116-112">Run `docker login` to log in to your container registry with your [registry credentials](container-registry-authentication.md).</span></span>

<span data-ttu-id="aa116-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="aa116-113">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="aa116-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span><span class="sxs-lookup"><span data-stu-id="aa116-114">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

> [!TIP]
> <span data-ttu-id="aa116-115">Make sure to specify the fully qualified registry name (all lowercase).</span><span class="sxs-lookup"><span data-stu-id="aa116-115">Make sure to specify the fully qualified registry name (all lowercase).</span></span> <span data-ttu-id="aa116-116">In this example, it is `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="aa116-116">In this example, it is `myregistry.azurecr.io`.</span></span>

## <a name="steps-to-pull-and-push-an-image"></a><span data-ttu-id="aa116-117">Steps to pull and push an image</span><span class="sxs-lookup"><span data-stu-id="aa116-117">Steps to pull and push an image</span></span>
<span data-ttu-id="aa116-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span><span class="sxs-lookup"><span data-stu-id="aa116-118">The follow example downloads the Nginx image from the public Docker Hub registry, tags it for your private Azure container registry, pushes it to your registry, then pulls it again.</span></span>

<span data-ttu-id="aa116-119">**1. Pull the Docker official image for Nginx**</span><span class="sxs-lookup"><span data-stu-id="aa116-119">**1. Pull the Docker official image for Nginx**</span></span>

<span data-ttu-id="aa116-120">First pull the public Nginx image to your local computer.</span><span class="sxs-lookup"><span data-stu-id="aa116-120">First pull the public Nginx image to your local computer.</span></span>

```
docker pull nginx
```
<span data-ttu-id="aa116-121">**2. Start the Nginx container**</span><span class="sxs-lookup"><span data-stu-id="aa116-121">**2. Start the Nginx container**</span></span>

<span data-ttu-id="aa116-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span><span class="sxs-lookup"><span data-stu-id="aa116-122">The following command starts the local Nginx container interactively on port 8080, allowing you to see output from Nginx.</span></span> <span data-ttu-id="aa116-123">It removes the running container once stopped.</span><span class="sxs-lookup"><span data-stu-id="aa116-123">It removes the running container once stopped.</span></span>

```
docker run -it --rm -p 8080:80 nginx
```

<span data-ttu-id="aa116-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span><span class="sxs-lookup"><span data-stu-id="aa116-124">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span> <span data-ttu-id="aa116-125">You see a screen similar to the following one.</span><span class="sxs-lookup"><span data-stu-id="aa116-125">You see a screen similar to the following one.</span></span>

![Nginx on local computer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-docker-cli/nginx.png)

<span data-ttu-id="aa116-127">To stop the running container, press [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="aa116-127">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="aa116-128">**3. Create an alias of the image in your registry**</span><span class="sxs-lookup"><span data-stu-id="aa116-128">**3. Create an alias of the image in your registry**</span></span>

<span data-ttu-id="aa116-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span><span class="sxs-lookup"><span data-stu-id="aa116-129">The following command creates an alias of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="aa116-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span><span class="sxs-lookup"><span data-stu-id="aa116-130">This example specifies the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```
docker tag nginx myregistry.azurecr.io/samples/nginx
```  

<span data-ttu-id="aa116-131">**4. Push the image to your registry**</span><span class="sxs-lookup"><span data-stu-id="aa116-131">**4. Push the image to your registry**</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="aa116-132">**5. Pull the image from your registry**</span><span class="sxs-lookup"><span data-stu-id="aa116-132">**5. Pull the image from your registry**</span></span>

```
docker pull myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="aa116-133">**6. Start the Nginx container from your registry**</span><span class="sxs-lookup"><span data-stu-id="aa116-133">**6. Start the Nginx container from your registry**</span></span>

```
docker run -it --rm -p 8080:80 myregistry.azurecr.io/samples/nginx
```

<span data-ttu-id="aa116-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span><span class="sxs-lookup"><span data-stu-id="aa116-134">Browse to [http://localhost:8080](http://localhost:8080) to view the running container.</span></span>

<span data-ttu-id="aa116-135">To stop the running container, press [CTRL]+[C].</span><span class="sxs-lookup"><span data-stu-id="aa116-135">To stop the running container, press [CTRL]+[C].</span></span>

<span data-ttu-id="aa116-136">**7. (Optional) Remove the image**</span><span class="sxs-lookup"><span data-stu-id="aa116-136">**7. (Optional) Remove the image**</span></span>

```
docker rmi myregistry.azurecr.io/samples/nginx
```

##<a name="concurrent-limits"></a><span data-ttu-id="aa116-137">Concurrent Limits</span><span class="sxs-lookup"><span data-stu-id="aa116-137">Concurrent Limits</span></span>
<span data-ttu-id="aa116-138">In some scenarios, executing calls concurrently might result in errors.</span><span class="sxs-lookup"><span data-stu-id="aa116-138">In some scenarios, executing calls concurrently might result in errors.</span></span> <span data-ttu-id="aa116-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span><span class="sxs-lookup"><span data-stu-id="aa116-139">The following table contains the limits of concurrent calls with "Push" and "Pull" operations on Azure container registry:</span></span>

| <span data-ttu-id="aa116-140">Operation</span><span class="sxs-lookup"><span data-stu-id="aa116-140">Operation</span></span>  | <span data-ttu-id="aa116-141">Limit</span><span class="sxs-lookup"><span data-stu-id="aa116-141">Limit</span></span>                                  |
| ---------- | -------------------------------------- |
| <span data-ttu-id="aa116-142">PULL</span><span class="sxs-lookup"><span data-stu-id="aa116-142">PULL</span></span>       | <span data-ttu-id="aa116-143">Up to 10 concurrent pulls per registry</span><span class="sxs-lookup"><span data-stu-id="aa116-143">Up to 10 concurrent pulls per registry</span></span> |
| <span data-ttu-id="aa116-144">PUSH</span><span class="sxs-lookup"><span data-stu-id="aa116-144">PUSH</span></span>       | <span data-ttu-id="aa116-145">Up to 5 concurrent pushes per registry</span><span class="sxs-lookup"><span data-stu-id="aa116-145">Up to 5 concurrent pushes per registry</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aa116-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa116-146">Next steps</span></span>
<span data-ttu-id="aa116-147">Now that you know the basics, you are ready to start using your registry!</span><span class="sxs-lookup"><span data-stu-id="aa116-147">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="aa116-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="aa116-148">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>

