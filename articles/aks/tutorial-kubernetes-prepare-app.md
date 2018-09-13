---
title: Kubernetes on Azure tutorial  - Prepare an application
description: In this Azure Kubernetes Service (AKS) tutorial, you learn how to prepare and build a multi-container app with Docker Compose that you can then deploy to AKS.
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: tutorial
ms.date: 08/14/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: b2bb187e5ad55b466da0b9b06ffbb047ac539717
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866705"
---
# <a name="tutorial-prepare-an-application-for-azure-kubernetes-service-aks"></a><span data-ttu-id="66e1e-103">Tutorial: Prepare an application for Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="66e1e-103">Tutorial: Prepare an application for Azure Kubernetes Service (AKS)</span></span>

<span data-ttu-id="66e1e-104">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="66e1e-104">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="66e1e-105">Existing development tools such as Docker Compose are used to locally build and test an application.</span><span class="sxs-lookup"><span data-stu-id="66e1e-105">Existing development tools such as Docker Compose are used to locally build and test an application.</span></span> <span data-ttu-id="66e1e-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="66e1e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="66e1e-107">Clone a sample application source from GitHub</span><span class="sxs-lookup"><span data-stu-id="66e1e-107">Clone a sample application source from GitHub</span></span>
> * <span data-ttu-id="66e1e-108">Create a container image from the sample application source</span><span class="sxs-lookup"><span data-stu-id="66e1e-108">Create a container image from the sample application source</span></span>
> * <span data-ttu-id="66e1e-109">Test the multi-container application in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="66e1e-109">Test the multi-container application in a local Docker environment</span></span>

<span data-ttu-id="66e1e-110">Once completed, the following application runs in your local development environment:</span><span class="sxs-lookup"><span data-stu-id="66e1e-110">Once completed, the following application runs in your local development environment:</span></span>

![Image of Kubernetes cluster on Azure](./media/container-service-tutorial-kubernetes-prepare-app/azure-vote.png)

<span data-ttu-id="66e1e-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then deployed into an AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="66e1e-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then deployed into an AKS cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="66e1e-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="66e1e-113">Before you begin</span></span>

<span data-ttu-id="66e1e-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and `docker` commands.</span><span class="sxs-lookup"><span data-stu-id="66e1e-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and `docker` commands.</span></span> <span data-ttu-id="66e1e-115">For a primer on container basics, see [Get started with Docker][docker-get-started].</span><span class="sxs-lookup"><span data-stu-id="66e1e-115">For a primer on container basics, see [Get started with Docker][docker-get-started].</span></span>

<span data-ttu-id="66e1e-116">To complete this tutorial, you need a local Docker development environment.</span><span class="sxs-lookup"><span data-stu-id="66e1e-116">To complete this tutorial, you need a local Docker development environment.</span></span> <span data-ttu-id="66e1e-117">Docker provides packages that configure Docker on a [Mac][docker-for-mac], [Windows][docker-for-windows], or [Linux][docker-for-linux] system.</span><span class="sxs-lookup"><span data-stu-id="66e1e-117">Docker provides packages that configure Docker on a [Mac][docker-for-mac], [Windows][docker-for-windows], or [Linux][docker-for-linux] system.</span></span>

<span data-ttu-id="66e1e-118">Azure Cloud Shell does not include the Docker components required to complete every step in these tutorials.</span><span class="sxs-lookup"><span data-stu-id="66e1e-118">Azure Cloud Shell does not include the Docker components required to complete every step in these tutorials.</span></span> <span data-ttu-id="66e1e-119">Therefore, we recommend using a full Docker development environment.</span><span class="sxs-lookup"><span data-stu-id="66e1e-119">Therefore, we recommend using a full Docker development environment.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="66e1e-120">Get application code</span><span class="sxs-lookup"><span data-stu-id="66e1e-120">Get application code</span></span>

<span data-ttu-id="66e1e-121">The sample application used in this tutorial is a basic voting app.</span><span class="sxs-lookup"><span data-stu-id="66e1e-121">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="66e1e-122">The application consists of a front-end web component and a back-end Redis instance.</span><span class="sxs-lookup"><span data-stu-id="66e1e-122">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="66e1e-123">The web component is packaged into a custom container image.</span><span class="sxs-lookup"><span data-stu-id="66e1e-123">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="66e1e-124">The Redis instance uses an unmodified image from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="66e1e-124">The Redis instance uses an unmodified image from Docker Hub.</span></span>

<span data-ttu-id="66e1e-125">Use [git][] to clone the sample application to your development environment:</span><span class="sxs-lookup"><span data-stu-id="66e1e-125">Use [git][] to clone the sample application to your development environment:</span></span>

```console
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="66e1e-126">Change directories so that you are working from the cloned directory.</span><span class="sxs-lookup"><span data-stu-id="66e1e-126">Change directories so that you are working from the cloned directory.</span></span>

```console
cd azure-voting-app-redis
```

<span data-ttu-id="66e1e-127">Inside the directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span><span class="sxs-lookup"><span data-stu-id="66e1e-127">Inside the directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="66e1e-128">These files are used throughout the tutorial set.</span><span class="sxs-lookup"><span data-stu-id="66e1e-128">These files are used throughout the tutorial set.</span></span>

## <a name="create-container-images"></a><span data-ttu-id="66e1e-129">Create container images</span><span class="sxs-lookup"><span data-stu-id="66e1e-129">Create container images</span></span>

<span data-ttu-id="66e1e-130">[Docker Compose][docker-compose] can be used to automate building container images and the deployment of multi-container applications.</span><span class="sxs-lookup"><span data-stu-id="66e1e-130">[Docker Compose][docker-compose] can be used to automate building container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="66e1e-131">Use the sample `docker-compose.yaml` file to create the container image, download the Redis image, and start the application:</span><span class="sxs-lookup"><span data-stu-id="66e1e-131">Use the sample `docker-compose.yaml` file to create the container image, download the Redis image, and start the application:</span></span>

```console
docker-compose up -d
```

<span data-ttu-id="66e1e-132">When completed, use the [docker images][docker-images] command to see the created images.</span><span class="sxs-lookup"><span data-stu-id="66e1e-132">When completed, use the [docker images][docker-images] command to see the created images.</span></span> <span data-ttu-id="66e1e-133">Three images have been downloaded or created.</span><span class="sxs-lookup"><span data-stu-id="66e1e-133">Three images have been downloaded or created.</span></span> <span data-ttu-id="66e1e-134">The *azure-vote-front* image contains the front-end application and uses the `nginx-flask` image as a base.</span><span class="sxs-lookup"><span data-stu-id="66e1e-134">The *azure-vote-front* image contains the front-end application and uses the `nginx-flask` image as a base.</span></span> <span data-ttu-id="66e1e-135">The `redis` image is used to start a Redis instance.</span><span class="sxs-lookup"><span data-stu-id="66e1e-135">The `redis` image is used to start a Redis instance.</span></span>

```
$ docker images

REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="66e1e-136">Run the [docker ps][docker-ps] command to see the running containers:</span><span class="sxs-lookup"><span data-stu-id="66e1e-136">Run the [docker ps][docker-ps] command to see the running containers:</span></span>

```
$ docker ps

CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="66e1e-137">Test application locally</span><span class="sxs-lookup"><span data-stu-id="66e1e-137">Test application locally</span></span>

<span data-ttu-id="66e1e-138">To see the running application, enter http://localhost:8080 in a local web browser.</span><span class="sxs-lookup"><span data-stu-id="66e1e-138">To see the running application, enter http://localhost:8080 in a local web browser.</span></span> <span data-ttu-id="66e1e-139">The sample application loads, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="66e1e-139">The sample application loads, as shown in the following example:</span></span>

![Image of Kubernetes cluster on Azure](./media/container-service-tutorial-kubernetes-prepare-app/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="66e1e-141">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="66e1e-141">Clean up resources</span></span>

<span data-ttu-id="66e1e-142">Now that the application's functionality has been validated, the running containers can be stopped and removed.</span><span class="sxs-lookup"><span data-stu-id="66e1e-142">Now that the application's functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="66e1e-143">Do not delete the container images - in the next tutorial, the *azure-vote-front* image is uploaded to an Azure Container Registry instance.</span><span class="sxs-lookup"><span data-stu-id="66e1e-143">Do not delete the container images - in the next tutorial, the *azure-vote-front* image is uploaded to an Azure Container Registry instance.</span></span>

<span data-ttu-id="66e1e-144">Stop and remove the container instances and resources with the [docker-compose down][docker-compose-down] command:</span><span class="sxs-lookup"><span data-stu-id="66e1e-144">Stop and remove the container instances and resources with the [docker-compose down][docker-compose-down] command:</span></span>

```console
docker-compose down
```

<span data-ttu-id="66e1e-145">When the local application has been removed, you have a Docker image that contains the Azure Vote application, *azure-front-front*, for use with the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="66e1e-145">When the local application has been removed, you have a Docker image that contains the Azure Vote application, *azure-front-front*, for use with the next tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66e1e-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="66e1e-146">Next steps</span></span>

<span data-ttu-id="66e1e-147">In this tutorial, an application was tested and container images created for the application.</span><span class="sxs-lookup"><span data-stu-id="66e1e-147">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="66e1e-148">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="66e1e-148">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="66e1e-149">Clone a sample application source from GitHub</span><span class="sxs-lookup"><span data-stu-id="66e1e-149">Clone a sample application source from GitHub</span></span>
> * <span data-ttu-id="66e1e-150">Create a container image from the sample application source</span><span class="sxs-lookup"><span data-stu-id="66e1e-150">Create a container image from the sample application source</span></span>
> * <span data-ttu-id="66e1e-151">Test the multi-container application in a local Docker environment</span><span class="sxs-lookup"><span data-stu-id="66e1e-151">Test the multi-container application in a local Docker environment</span></span>

<span data-ttu-id="66e1e-152">Advance to the next tutorial to learn how to store container images in Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="66e1e-152">Advance to the next tutorial to learn how to store container images in Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="66e1e-153">[Push images to Azure Container Registry][aks-tutorial-prepare-acr]</span><span class="sxs-lookup"><span data-stu-id="66e1e-153">[Push images to Azure Container Registry][aks-tutorial-prepare-acr]</span></span>

<!-- LINKS - external -->
[docker-compose]: https://docs.docker.com/compose/
[docker-for-linux]: https://docs.docker.com/engine/installation/#supported-platforms
[docker-for-mac]: https://docs.docker.com/docker-for-mac/
[docker-for-windows]: https://docs.docker.com/docker-for-windows/
[docker-get-started]: https://docs.docker.com/get-started/
[docker-images]: https://docs.docker.com/engine/reference/commandline/images/
[docker-ps]: https://docs.docker.com/engine/reference/commandline/ps/
[docker-compose-down]: https://docs.docker.com/compose/reference/down
[git]: https://git-scm.com/downloads

<!-- LINKS - internal -->
[aks-tutorial-prepare-acr]: ./tutorial-kubernetes-prepare-acr.md
