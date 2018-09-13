---
title: Private Docker container registries in Azure | Microsoft Docs
description: Introduction to the Azure Container Registry service, providing cloud-based, managed, private Docker registries.
services: container-registry
documentationcenter: ''
author: stevelas
manager: balans
editor: dlepow
tags: ''
keywords: ''
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2016
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25301f1bbacdf2f1e3d04ed3470eafd31098ea32
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563565"
---
# <a name="introduction-to-private-docker-container-registries"></a><span data-ttu-id="c2fc7-103">Introduction to private Docker container registries</span><span class="sxs-lookup"><span data-stu-id="c2fc7-103">Introduction to private Docker container registries</span></span>


<span data-ttu-id="c2fc7-104">Azure Container Registry is a managed [Docker registry](https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-104">Azure Container Registry is a managed [Docker registry](https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="c2fc7-105">Create and maintain Azure container registries to store and manage your private [Docker container](https://www.docker.com/what-docker) images.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-105">Create and maintain Azure container registries to store and manage your private [Docker container](https://www.docker.com/what-docker) images.</span></span> <span data-ttu-id="c2fc7-106">Use container registries in Azure with your existing container development and deployment pipelines, and draw on the body of Docker community expertise.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-106">Use container registries in Azure with your existing container development and deployment pipelines, and draw on the body of Docker community expertise.</span></span>

<span data-ttu-id="c2fc7-107">For background about Docker and containers, see:</span><span class="sxs-lookup"><span data-stu-id="c2fc7-107">For background about Docker and containers, see:</span></span>

* [<span data-ttu-id="c2fc7-108">Docker user guide</span><span class="sxs-lookup"><span data-stu-id="c2fc7-108">Docker user guide</span></span>](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a><span data-ttu-id="c2fc7-109">Use cases</span><span class="sxs-lookup"><span data-stu-id="c2fc7-109">Use cases</span></span>
<span data-ttu-id="c2fc7-110">Pull images from an Azure container registry to various deployment targets:</span><span class="sxs-lookup"><span data-stu-id="c2fc7-110">Pull images from an Azure container registry to various deployment targets:</span></span>

* <span data-ttu-id="c2fc7-111">**Scalable orchestration systems** that manage containerized applications across clusters of hosts, including [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/), and [Kubernetes](http://kubernetes.io/docs/).</span><span class="sxs-lookup"><span data-stu-id="c2fc7-111">**Scalable orchestration systems** that manage containerized applications across clusters of hosts, including [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/), and [Kubernetes](http://kubernetes.io/docs/).</span></span>
* <span data-ttu-id="c2fc7-112">**Azure services** that support building and running applications at scale, including [Container Service](../container-service/index.md), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](../service-fabric/index.md), and others.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-112">**Azure services** that support building and running applications at scale, including [Container Service](../container-service/index.md), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](../service-fabric/index.md), and others.</span></span>

<span data-ttu-id="c2fc7-113">Developers can also push to a container registry as part of a container development workflow.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-113">Developers can also push to a container registry as part of a container development workflow.</span></span> <span data-ttu-id="c2fc7-114">For example, target a container registry from a continuous integration and deployment tool such as [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) or [Jenkins](https://jenkins.io/).</span><span class="sxs-lookup"><span data-stu-id="c2fc7-114">For example, target a container registry from a continuous integration and deployment tool such as [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) or [Jenkins](https://jenkins.io/).</span></span>





## <a name="key-concepts"></a><span data-ttu-id="c2fc7-115">Key concepts</span><span class="sxs-lookup"><span data-stu-id="c2fc7-115">Key concepts</span></span>
* <span data-ttu-id="c2fc7-116">**Registry** - Create one or more container registries in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-116">**Registry** - Create one or more container registries in your Azure subscription.</span></span> <span data-ttu-id="c2fc7-117">Each registry is backed by a standard Azure [storage account](../storage/storage-introduction.md) in the same location.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-117">Each registry is backed by a standard Azure [storage account](../storage/storage-introduction.md) in the same location.</span></span> <span data-ttu-id="c2fc7-118">Take advantage of local, network-close storage of your container images by creating a registry in the same Azure location as your deployments.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-118">Take advantage of local, network-close storage of your container images by creating a registry in the same Azure location as your deployments.</span></span> <span data-ttu-id="c2fc7-119">A fully qualified registry name has the form `myregistry.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-119">A fully qualified registry name has the form `myregistry.azurecr.io`.</span></span>

  <span data-ttu-id="c2fc7-120">You [control access](container-registry-authentication.md) to a container registry using an Azure Active Directory-backed [service principal](../active-directory/active-directory-application-objects.md) or a provided admin account.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-120">You [control access](container-registry-authentication.md) to a container registry using an Azure Active Directory-backed [service principal](../active-directory/active-directory-application-objects.md) or a provided admin account.</span></span> <span data-ttu-id="c2fc7-121">Run the standard `docker login` command to authenticate with a registry.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-121">Run the standard `docker login` command to authenticate with a registry.</span></span>

* <span data-ttu-id="c2fc7-122">**Repository** - A registry contains one or more repositories, which are groups of container images.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-122">**Repository** - A registry contains one or more repositories, which are groups of container images.</span></span> <span data-ttu-id="c2fc7-123">Azure Container Registry supports multilevel repository namespaces.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-123">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="c2fc7-124">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-124">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="c2fc7-125">For example:</span><span class="sxs-lookup"><span data-stu-id="c2fc7-125">For example:</span></span>

  * <span data-ttu-id="c2fc7-126">`myregistry.azurecr.io/aspnetcore:1.0.1` represents a corporate-wide image</span><span class="sxs-lookup"><span data-stu-id="c2fc7-126">`myregistry.azurecr.io/aspnetcore:1.0.1` represents a corporate-wide image</span></span>
  * <span data-ttu-id="c2fc7-127">`myregistry.azurecr.io/warrantydept/dotnet-build` represents an image used to build .NET apps, shared across the warranty department</span><span class="sxs-lookup"><span data-stu-id="c2fc7-127">`myregistry.azurecr.io/warrantydept/dotnet-build` represents an image used to build .NET apps, shared across the warranty department</span></span>
  * <span data-ttu-id="c2fc7-128">`myregistry.azrecr.io/warrantydept/customersubmissions/web` represents a web image, grouped in the customer submissions app, owned by the warranty department</span><span class="sxs-lookup"><span data-stu-id="c2fc7-128">`myregistry.azrecr.io/warrantydept/customersubmissions/web` represents a web image, grouped in the customer submissions app, owned by the warranty department</span></span>

* <span data-ttu-id="c2fc7-129">**Image** - Stored in a repository, each image is a read-only snapshot of a Docker container.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-129">**Image** - Stored in a repository, each image is a read-only snapshot of a Docker container.</span></span> <span data-ttu-id="c2fc7-130">Azure container registries can include both Windows and Linux images.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-130">Azure container registries can include both Windows and Linux images.</span></span> <span data-ttu-id="c2fc7-131">You control image names for all your container deployments.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-131">You control image names for all your container deployments.</span></span> <span data-ttu-id="c2fc7-132">Use standard [Docker commands](https://docs.docker.com/engine/reference/commandline/) to push images into a repository, or pull an image from a repository.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-132">Use standard [Docker commands](https://docs.docker.com/engine/reference/commandline/) to push images into a repository, or pull an image from a repository.</span></span>

* <span data-ttu-id="c2fc7-133">**Container** - A container defines a software application and its dependencies wrapped in a complete filesystem including code, runtime, system tools, and libraries.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-133">**Container** - A container defines a software application and its dependencies wrapped in a complete filesystem including code, runtime, system tools, and libraries.</span></span> <span data-ttu-id="c2fc7-134">Run Docker containers based on Windows or Linux images that you pull from a container registry.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-134">Run Docker containers based on Windows or Linux images that you pull from a container registry.</span></span> <span data-ttu-id="c2fc7-135">Containers running on a single machine share the operating system kernel.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-135">Containers running on a single machine share the operating system kernel.</span></span> <span data-ttu-id="c2fc7-136">Docker containers are fully portable to all major Linux distros, Mac, and Windows.</span><span class="sxs-lookup"><span data-stu-id="c2fc7-136">Docker containers are fully portable to all major Linux distros, Mac, and Windows.</span></span>




## <a name="next-steps"></a><span data-ttu-id="c2fc7-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2fc7-137">Next steps</span></span>
* [<span data-ttu-id="c2fc7-138">Create a container registry using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c2fc7-138">Create a container registry using the Azure portal</span></span>](container-registry-get-started-portal.md)
* [<span data-ttu-id="c2fc7-139">Create a container registry using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c2fc7-139">Create a container registry using the Azure CLI</span></span>](container-registry-get-started-azure-cli.md)
* [<span data-ttu-id="c2fc7-140">Push your first image using the Docker CLI</span><span class="sxs-lookup"><span data-stu-id="c2fc7-140">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
* <span data-ttu-id="c2fc7-141">To build a continuous integration and deployment workflow using Visual Studio Team Services, Azure Container Service, and Azure Container Registry, see [this tutorial](../container-service/container-service-setup-ci-cd.md).</span><span class="sxs-lookup"><span data-stu-id="c2fc7-141">To build a continuous integration and deployment workflow using Visual Studio Team Services, Azure Container Service, and Azure Container Registry, see [this tutorial](../container-service/container-service-setup-ci-cd.md).</span></span>
* <span data-ttu-id="c2fc7-142">If you want to set up your own Docker private registry in Azure (without a public endpoint), see [Deploying Your Own Private Docker Registry on Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="c2fc7-142">If you want to set up your own Docker private registry in Azure (without a public endpoint), see [Deploying Your Own Private Docker Registry on Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).</span></span>
