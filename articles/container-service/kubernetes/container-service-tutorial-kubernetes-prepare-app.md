---
title: Azure Container Service tutorial - Prepare App
description: Azure Container Service tutorial - Prepare App
services: container-service
author: neilpeterson
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 02/26/2018
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2fe160652bf8df289d590722ef4024f0b3dd397c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867670"
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a><span data-ttu-id="5ce62-103">Create container images to be used with Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="5ce62-103">Create container images to be used with Azure Container Service</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="5ce62-104">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5ce62-104">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="5ce62-105">Steps completed include:</span><span class="sxs-lookup"><span data-stu-id="5ce62-105">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="5ce62-106">Cloning application source from GitHub</span><span class="sxs-lookup"><span data-stu-id="5ce62-106">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="5ce62-107">Creating a container image from the application source</span><span class="sxs-lookup"><span data-stu-id="5ce62-107">Creating a container image from the application source</span></span>
> * <span data-ttu-id="5ce62-108">Testing the application in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="5ce62-108">Testing the application in a local Docker environment</span></span>

<span data-ttu-id="5ce62-109">Once completed, the following application is accessible in your local development environment.</span><span class="sxs-lookup"><span data-stu-id="5ce62-109">Once completed, the following application is accessible in your local development environment.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="5ce62-111">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="5ce62-111">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5ce62-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5ce62-112">Before you begin</span></span>

<span data-ttu-id="5ce62-113">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span><span class="sxs-lookup"><span data-stu-id="5ce62-113">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="5ce62-114">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span><span class="sxs-lookup"><span data-stu-id="5ce62-114">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="5ce62-115">To complete this tutorial, you need a Docker development environment.</span><span class="sxs-lookup"><span data-stu-id="5ce62-115">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="5ce62-116">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span><span class="sxs-lookup"><span data-stu-id="5ce62-116">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

<span data-ttu-id="5ce62-117">Azure Cloud Shell does not include the Docker components required to complete every step this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ce62-117">Azure Cloud Shell does not include the Docker components required to complete every step this tutorial.</span></span> <span data-ttu-id="5ce62-118">Therefore, we recommend using a full Docker development environment.</span><span class="sxs-lookup"><span data-stu-id="5ce62-118">Therefore, we recommend using a full Docker development environment.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="5ce62-119">Get application code</span><span class="sxs-lookup"><span data-stu-id="5ce62-119">Get application code</span></span>

<span data-ttu-id="5ce62-120">The sample application used in this tutorial is a basic voting app.</span><span class="sxs-lookup"><span data-stu-id="5ce62-120">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="5ce62-121">The application consists of a front-end web component and a back-end Redis instance.</span><span class="sxs-lookup"><span data-stu-id="5ce62-121">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="5ce62-122">The web component is packaged into a custom container image.</span><span class="sxs-lookup"><span data-stu-id="5ce62-122">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="5ce62-123">The Redis instance uses an unmodified image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="5ce62-123">The Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="5ce62-124">Use git to download a copy of the application to your development environment.</span><span class="sxs-lookup"><span data-stu-id="5ce62-124">Use git to download a copy of the application to your development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="5ce62-125">Change directories so that you are working from the cloned directory.</span><span class="sxs-lookup"><span data-stu-id="5ce62-125">Change directories so that you are working from the cloned directory.</span></span>

```
cd azure-voting-app-redis
```

<span data-ttu-id="5ce62-126">Inside the directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span><span class="sxs-lookup"><span data-stu-id="5ce62-126">Inside the directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="5ce62-127">These files are used throughout the tutorial set.</span><span class="sxs-lookup"><span data-stu-id="5ce62-127">These files are used throughout the tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="5ce62-128">Create container images</span><span class="sxs-lookup"><span data-stu-id="5ce62-128">Create container images</span></span>

<span data-ttu-id="5ce62-129">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span><span class="sxs-lookup"><span data-stu-id="5ce62-129">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="5ce62-130">Run the `docker-compose.yml` file to create the container image, download the Redis image, and start the application.</span><span class="sxs-lookup"><span data-stu-id="5ce62-130">Run the `docker-compose.yml` file to create the container image, download the Redis image, and start the application.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="5ce62-131">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span><span class="sxs-lookup"><span data-stu-id="5ce62-131">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span></span>

```bash
docker images
```

<span data-ttu-id="5ce62-132">Notice that three images have been downloaded or created.</span><span class="sxs-lookup"><span data-stu-id="5ce62-132">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="5ce62-133">The `azure-vote-front` image contains the application and uses the `nginx-flask` image as a base.</span><span class="sxs-lookup"><span data-stu-id="5ce62-133">The `azure-vote-front` image contains the application and uses the `nginx-flask` image as a base.</span></span> <span data-ttu-id="5ce62-134">The `redis` image is used to start a Redis instance.</span><span class="sxs-lookup"><span data-stu-id="5ce62-134">The `redis` image is used to start a Redis instance.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="5ce62-135">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span><span class="sxs-lookup"><span data-stu-id="5ce62-135">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="5ce62-136">Output:</span><span class="sxs-lookup"><span data-stu-id="5ce62-136">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="5ce62-137">Test application locally</span><span class="sxs-lookup"><span data-stu-id="5ce62-137">Test application locally</span></span>

<span data-ttu-id="5ce62-138">Browse to http://localhost:8080 to see the running application.</span><span class="sxs-lookup"><span data-stu-id="5ce62-138">Browse to http://localhost:8080 to see the running application.</span></span>

![Image of Kubernetes cluster on Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="5ce62-140">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="5ce62-140">Clean up resources</span></span>

<span data-ttu-id="5ce62-141">Now that application functionality has been validated, the running containers can be stopped and removed.</span><span class="sxs-lookup"><span data-stu-id="5ce62-141">Now that application functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="5ce62-142">Do not delete the container images.</span><span class="sxs-lookup"><span data-stu-id="5ce62-142">Do not delete the container images.</span></span> <span data-ttu-id="5ce62-143">The `azure-vote-front` image is uploaded to an Azure Container Registry instance in the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ce62-143">The `azure-vote-front` image is uploaded to an Azure Container Registry instance in the next tutorial.</span></span>

<span data-ttu-id="5ce62-144">Run the following to stop the running containers.</span><span class="sxs-lookup"><span data-stu-id="5ce62-144">Run the following to stop the running containers.</span></span>

```bash
docker-compose stop
```

<span data-ttu-id="5ce62-145">Delete the stopped containers and resources with the following command.</span><span class="sxs-lookup"><span data-stu-id="5ce62-145">Delete the stopped containers and resources with the following command.</span></span>

```bash
docker-compose down
```

<span data-ttu-id="5ce62-146">At completion, you have a container image that contains the Azure Vote application.</span><span class="sxs-lookup"><span data-stu-id="5ce62-146">At completion, you have a container image that contains the Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ce62-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ce62-147">Next steps</span></span>

<span data-ttu-id="5ce62-148">In this tutorial, an application was tested and container images created for the application.</span><span class="sxs-lookup"><span data-stu-id="5ce62-148">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="5ce62-149">The following steps were completed:</span><span class="sxs-lookup"><span data-stu-id="5ce62-149">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5ce62-150">Cloning the application source from GitHub</span><span class="sxs-lookup"><span data-stu-id="5ce62-150">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="5ce62-151">Created a container image from application source</span><span class="sxs-lookup"><span data-stu-id="5ce62-151">Created a container image from application source</span></span>
> * <span data-ttu-id="5ce62-152">Tested the application in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="5ce62-152">Tested the application in a local Docker environment</span></span>

<span data-ttu-id="5ce62-153">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="5ce62-153">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ce62-154">Push images to Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="5ce62-154">Push images to Azure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
