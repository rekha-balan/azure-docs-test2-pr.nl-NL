---
title: Image storage in Azure Container Registry
description: Details on how your Docker container images are stored in Azure Container Registry, including security, redundancy, and capacity.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 03/21/2018
ms.author: marsma
ms.openlocfilehash: 65ff60be992440c69e50a084b467a8efbb19574e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867941"
---
# <a name="container-image-storage-in-azure-container-registry"></a><span data-ttu-id="be4b7-103">Container image storage in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="be4b7-103">Container image storage in Azure Container Registry</span></span>

<span data-ttu-id="be4b7-104">Every [Basic, Standard, and Premium](container-registry-skus.md) Azure container registry benefits from advanced Azure storage features like encryption-at-rest for image data security and geo-redundancy for image data protection.</span><span class="sxs-lookup"><span data-stu-id="be4b7-104">Every [Basic, Standard, and Premium](container-registry-skus.md) Azure container registry benefits from advanced Azure storage features like encryption-at-rest for image data security and geo-redundancy for image data protection.</span></span> <span data-ttu-id="be4b7-105">The following sections describe both the features and limits of image storage in Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="be4b7-105">The following sections describe both the features and limits of image storage in Azure Container Registry (ACR).</span></span>

## <a name="encryption-at-rest"></a><span data-ttu-id="be4b7-106">Encryption-at-rest</span><span class="sxs-lookup"><span data-stu-id="be4b7-106">Encryption-at-rest</span></span>

<span data-ttu-id="be4b7-107">All container images in your registry are encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="be4b7-107">All container images in your registry are encrypted at rest.</span></span> <span data-ttu-id="be4b7-108">Azure automatically encrypts an image before storing it, and decrypts it on-the-fly when you or your applications and services pull the image.</span><span class="sxs-lookup"><span data-stu-id="be4b7-108">Azure automatically encrypts an image before storing it, and decrypts it on-the-fly when you or your applications and services pull the image.</span></span>

## <a name="geo-redundant-storage"></a><span data-ttu-id="be4b7-109">Geo-redundant storage</span><span class="sxs-lookup"><span data-stu-id="be4b7-109">Geo-redundant storage</span></span>

<span data-ttu-id="be4b7-110">Azure uses a geo-redundant storage scheme to guard against loss of your container images.</span><span class="sxs-lookup"><span data-stu-id="be4b7-110">Azure uses a geo-redundant storage scheme to guard against loss of your container images.</span></span> <span data-ttu-id="be4b7-111">Azure Container Registry automatically replicates your container images to multiple geographically distant data centers, preventing their loss in the event of a regional storage failure.</span><span class="sxs-lookup"><span data-stu-id="be4b7-111">Azure Container Registry automatically replicates your container images to multiple geographically distant data centers, preventing their loss in the event of a regional storage failure.</span></span>

## <a name="geo-replication"></a><span data-ttu-id="be4b7-112">Geo-replication</span><span class="sxs-lookup"><span data-stu-id="be4b7-112">Geo-replication</span></span>

<span data-ttu-id="be4b7-113">For scenarios requiring even more high-availability assurance, consider using the [geo-replication](container-registry-geo-replication.md) feature of Premium registries.</span><span class="sxs-lookup"><span data-stu-id="be4b7-113">For scenarios requiring even more high-availability assurance, consider using the [geo-replication](container-registry-geo-replication.md) feature of Premium registries.</span></span> <span data-ttu-id="be4b7-114">Geo-replication helps guard against losing access to your registry in the event of a *total* regional failure, not just a storage failure.</span><span class="sxs-lookup"><span data-stu-id="be4b7-114">Geo-replication helps guard against losing access to your registry in the event of a *total* regional failure, not just a storage failure.</span></span> <span data-ttu-id="be4b7-115">Geo-replication provides other benefits, too, like network-close image storage for faster pushes and pulls in distributed development or deployment scenarios.</span><span class="sxs-lookup"><span data-stu-id="be4b7-115">Geo-replication provides other benefits, too, like network-close image storage for faster pushes and pulls in distributed development or deployment scenarios.</span></span>

## <a name="image-limits"></a><span data-ttu-id="be4b7-116">Image limits</span><span class="sxs-lookup"><span data-stu-id="be4b7-116">Image limits</span></span>

<span data-ttu-id="be4b7-117">The following table describes the container image and storage limits in place for Azure container registries.</span><span class="sxs-lookup"><span data-stu-id="be4b7-117">The following table describes the container image and storage limits in place for Azure container registries.</span></span>

| <span data-ttu-id="be4b7-118">Resource</span><span class="sxs-lookup"><span data-stu-id="be4b7-118">Resource</span></span> | <span data-ttu-id="be4b7-119">Limit</span><span class="sxs-lookup"><span data-stu-id="be4b7-119">Limit</span></span> |
| -------- | :---- |
| <span data-ttu-id="be4b7-120">Repositories</span><span class="sxs-lookup"><span data-stu-id="be4b7-120">Repositories</span></span> | <span data-ttu-id="be4b7-121">No limit</span><span class="sxs-lookup"><span data-stu-id="be4b7-121">No limit</span></span> |
| <span data-ttu-id="be4b7-122">Images</span><span class="sxs-lookup"><span data-stu-id="be4b7-122">Images</span></span> | <span data-ttu-id="be4b7-123">No limit</span><span class="sxs-lookup"><span data-stu-id="be4b7-123">No limit</span></span> |
| <span data-ttu-id="be4b7-124">Layers</span><span class="sxs-lookup"><span data-stu-id="be4b7-124">Layers</span></span> | <span data-ttu-id="be4b7-125">No limit</span><span class="sxs-lookup"><span data-stu-id="be4b7-125">No limit</span></span> |
| <span data-ttu-id="be4b7-126">Tags</span><span class="sxs-lookup"><span data-stu-id="be4b7-126">Tags</span></span> | <span data-ttu-id="be4b7-127">No limit</span><span class="sxs-lookup"><span data-stu-id="be4b7-127">No limit</span></span>|
| <span data-ttu-id="be4b7-128">Storage</span><span class="sxs-lookup"><span data-stu-id="be4b7-128">Storage</span></span> | <span data-ttu-id="be4b7-129">5 TB</span><span class="sxs-lookup"><span data-stu-id="be4b7-129">5 TB</span></span> |

<span data-ttu-id="be4b7-130">Very high numbers of repositories and tags can impact the performance of your registry.</span><span class="sxs-lookup"><span data-stu-id="be4b7-130">Very high numbers of repositories and tags can impact the performance of your registry.</span></span> <span data-ttu-id="be4b7-131">Periodically delete unused repositories, tags, and images as part of your registry maintenance routine.</span><span class="sxs-lookup"><span data-stu-id="be4b7-131">Periodically delete unused repositories, tags, and images as part of your registry maintenance routine.</span></span> <span data-ttu-id="be4b7-132">Deleted registry resources like repositories, images, and tags *cannot* be recovered after deletion.</span><span class="sxs-lookup"><span data-stu-id="be4b7-132">Deleted registry resources like repositories, images, and tags *cannot* be recovered after deletion.</span></span> <span data-ttu-id="be4b7-133">For more information about deleting registry resources, see [Delete container images in Azure Container Registry](container-registry-delete.md).</span><span class="sxs-lookup"><span data-stu-id="be4b7-133">For more information about deleting registry resources, see [Delete container images in Azure Container Registry](container-registry-delete.md).</span></span>

## <a name="storage-cost"></a><span data-ttu-id="be4b7-134">Storage cost</span><span class="sxs-lookup"><span data-stu-id="be4b7-134">Storage cost</span></span>

<span data-ttu-id="be4b7-135">For full details about pricing, see [Azure Container Registry pricing][pricing].</span><span class="sxs-lookup"><span data-stu-id="be4b7-135">For full details about pricing, see [Azure Container Registry pricing][pricing].</span></span>

## <a name="next-steps"></a><span data-ttu-id="be4b7-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="be4b7-136">Next steps</span></span>

<span data-ttu-id="be4b7-137">For more information about the different Azure Container Registry SKUs (Basic, Standard, Premium), see [Azure Container Registry SKUs](container-registry-skus.md).</span><span class="sxs-lookup"><span data-stu-id="be4b7-137">For more information about the different Azure Container Registry SKUs (Basic, Standard, Premium), see [Azure Container Registry SKUs](container-registry-skus.md).</span></span>

<!-- IMAGES -->

<!-- LINKS - External -->
[portal]: https://portal.azure.com
[pricing]: http://aka.ms/acr/pricing

<!-- LINKS - Internal -->
