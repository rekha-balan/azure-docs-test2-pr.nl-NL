---
title: Azure container registry repositories | Microsoft Docs
description: How to use Azure Container Registry repositories for Docker images
services: container-registry
documentationcenter: ''
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 8f4d4ae9efdb3af4cb134c6cc224b839dd80c674
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564064"
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="ace01-103">Azure container registry repositories</span><span class="sxs-lookup"><span data-stu-id="ace01-103">Azure container registry repositories</span></span>

<span data-ttu-id="ace01-104">Azure container registry allows you to store container images in repositories.</span><span class="sxs-lookup"><span data-stu-id="ace01-104">Azure container registry allows you to store container images in repositories.</span></span> <span data-ttu-id="ace01-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span><span class="sxs-lookup"><span data-stu-id="ace01-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="ace01-106">You can specify these repositories when you push images to your registry.</span><span class="sxs-lookup"><span data-stu-id="ace01-106">You can specify these repositories when you push images to your registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ace01-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ace01-107">Prerequisites</span></span>
* <span data-ttu-id="ace01-108">**Azure container registry** - Create a container registry in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ace01-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="ace01-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ace01-109">For example, use the [Azure portal](container-registry-get-started-portal.md) or the [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="ace01-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="ace01-110">**Docker CLI** - To set up your local computer as a Docker host and access the Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="ace01-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span><span class="sxs-lookup"><span data-stu-id="ace01-111">**Pull an image** - Pull an image from the public Docker Hub registry, tag it, and push it to your registry.</span></span> <span data-ttu-id="ace01-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ace01-112">For guidance on how push and pull images, see [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-the-portal"></a><span data-ttu-id="ace01-113">Viewing repositories in the Portal</span><span class="sxs-lookup"><span data-stu-id="ace01-113">Viewing repositories in the Portal</span></span>

<span data-ttu-id="ace01-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ace01-114">Once you have pushed images to your container registry, you can see a list of the repositories hosting the images in the Azure portal.</span></span>

<span data-ttu-id="ace01-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span><span class="sxs-lookup"><span data-stu-id="ace01-115">If you followed the steps in the [Push Docker image to Azure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="ace01-116">As part of the instructions, you should have specified a namespace for the image.</span><span class="sxs-lookup"><span data-stu-id="ace01-116">As part of the instructions, you should have specified a namespace for the image.</span></span> <span data-ttu-id="ace01-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span><span class="sxs-lookup"><span data-stu-id="ace01-117">In the example below, the command pushes the NGinx image to the "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="ace01-118">Azure Container Registry supports multilevel repository namespaces.</span><span class="sxs-lookup"><span data-stu-id="ace01-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="ace01-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span><span class="sxs-lookup"><span data-stu-id="ace01-119">This feature enables you to group collections of images related to a specific app, or a collection of apps to specific development or operational teams.</span></span> <span data-ttu-id="ace01-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ace01-120">To read more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="ace01-121">To view the container registry repositories:</span><span class="sxs-lookup"><span data-stu-id="ace01-121">To view the container registry repositories:</span></span>

1. <span data-ttu-id="ace01-122">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ace01-122">Log in to the Azure portal</span></span>
2. <span data-ttu-id="ace01-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span><span class="sxs-lookup"><span data-stu-id="ace01-123">On the **Azure Container Registry** blade, select the registry you wish to inspect</span></span>
3. <span data-ttu-id="ace01-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span><span class="sxs-lookup"><span data-stu-id="ace01-124">In the registry blade, click **Repositories** to see a list of all the repositories and their images</span></span>
4. <span data-ttu-id="ace01-125">(Optional) Select a specific image to see tags</span><span class="sxs-lookup"><span data-stu-id="ace01-125">(Optional) Select a specific image to see tags</span></span>

![Repositories in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="ace01-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="ace01-127">Next steps</span></span>
<span data-ttu-id="ace01-128">Now that you know the basics, you are ready to start using your registry!</span><span class="sxs-lookup"><span data-stu-id="ace01-128">Now that you know the basics, you are ready to start using your registry!</span></span> <span data-ttu-id="ace01-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span><span class="sxs-lookup"><span data-stu-id="ace01-129">For example, start deploying container images to an [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>

