---
title: Geo-replicating an Azure container registry
description: Get started creating and managing geo-replicated Azure container registries.
services: container-registry
author: stevelas
manager: jeconnoc
ms.service: container-registry
ms.topic: overview-article
ms.date: 04/10/2018
ms.author: stevelas
ms.openlocfilehash: e4695428b03961f5e899007609dfb1088dde77a8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866752"
---
# <a name="geo-replication-in-azure-container-registry"></a><span data-ttu-id="349a3-103">Geo-replication in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="349a3-103">Geo-replication in Azure Container Registry</span></span>

<span data-ttu-id="349a3-104">Companies that want a local presence, or a hot backup, choose to run services from multiple Azure regions.</span><span class="sxs-lookup"><span data-stu-id="349a3-104">Companies that want a local presence, or a hot backup, choose to run services from multiple Azure regions.</span></span> <span data-ttu-id="349a3-105">As a best practice, placing a container registry in each region where images are run allows network-close operations, enabling fast, reliable image layer transfers.</span><span class="sxs-lookup"><span data-stu-id="349a3-105">As a best practice, placing a container registry in each region where images are run allows network-close operations, enabling fast, reliable image layer transfers.</span></span> <span data-ttu-id="349a3-106">Geo-replication enables an Azure container registry to function as a single registry, serving multiple regions with multi-master regional registries.</span><span class="sxs-lookup"><span data-stu-id="349a3-106">Geo-replication enables an Azure container registry to function as a single registry, serving multiple regions with multi-master regional registries.</span></span>

<span data-ttu-id="349a3-107">A geo-replicated registry provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="349a3-107">A geo-replicated registry provides the following benefits:</span></span>

* <span data-ttu-id="349a3-108">Single registry/image/tag names can be used across multiple regions</span><span class="sxs-lookup"><span data-stu-id="349a3-108">Single registry/image/tag names can be used across multiple regions</span></span>
* <span data-ttu-id="349a3-109">Network-close registry access from regional deployments</span><span class="sxs-lookup"><span data-stu-id="349a3-109">Network-close registry access from regional deployments</span></span>
* <span data-ttu-id="349a3-110">No additional egress fees, as images are pulled from a local, replicated registry in the same region as your container host</span><span class="sxs-lookup"><span data-stu-id="349a3-110">No additional egress fees, as images are pulled from a local, replicated registry in the same region as your container host</span></span>
* <span data-ttu-id="349a3-111">Single management of a registry across multiple regions</span><span class="sxs-lookup"><span data-stu-id="349a3-111">Single management of a registry across multiple regions</span></span>

## <a name="example-use-case"></a><span data-ttu-id="349a3-112">Example use case</span><span class="sxs-lookup"><span data-stu-id="349a3-112">Example use case</span></span>
<span data-ttu-id="349a3-113">Contoso runs a public presence website located across the US, Canada, and Europe.</span><span class="sxs-lookup"><span data-stu-id="349a3-113">Contoso runs a public presence website located across the US, Canada, and Europe.</span></span> <span data-ttu-id="349a3-114">To serve these markets with local and network-close content, Contoso runs [Azure Container Service](/azure/container-service/kubernetes/) (ACS) Kubernetes clusters in West US, East US, Canada Central, and West Europe.</span><span class="sxs-lookup"><span data-stu-id="349a3-114">To serve these markets with local and network-close content, Contoso runs [Azure Container Service](/azure/container-service/kubernetes/) (ACS) Kubernetes clusters in West US, East US, Canada Central, and West Europe.</span></span> <span data-ttu-id="349a3-115">The website application, deployed as a Docker image, utilizes the same code and image across all regions.</span><span class="sxs-lookup"><span data-stu-id="349a3-115">The website application, deployed as a Docker image, utilizes the same code and image across all regions.</span></span> <span data-ttu-id="349a3-116">Content, local to that region, is retrieved from a database, which is provisioned uniquely in each region.</span><span class="sxs-lookup"><span data-stu-id="349a3-116">Content, local to that region, is retrieved from a database, which is provisioned uniquely in each region.</span></span> <span data-ttu-id="349a3-117">Each regional deployment has its unique configuration for resources like the local database.</span><span class="sxs-lookup"><span data-stu-id="349a3-117">Each regional deployment has its unique configuration for resources like the local database.</span></span>

<span data-ttu-id="349a3-118">The development team is located in Seattle WA, utilizing the West US data center.</span><span class="sxs-lookup"><span data-stu-id="349a3-118">The development team is located in Seattle WA, utilizing the West US data center.</span></span>

<span data-ttu-id="349a3-119">![Pushing to multiple registries](media/container-registry-geo-replication/before-geo-replicate.png)</span><span class="sxs-lookup"><span data-stu-id="349a3-119">![Pushing to multiple registries](media/container-registry-geo-replication/before-geo-replicate.png)</span></span><br /><span data-ttu-id="349a3-120">*Pushing to multiple registries*</span><span class="sxs-lookup"><span data-stu-id="349a3-120">*Pushing to multiple registries*</span></span>

<span data-ttu-id="349a3-121">Prior to using the geo-replication features, Contoso had a US-based registry in West US, with an additional registry in West Europe.</span><span class="sxs-lookup"><span data-stu-id="349a3-121">Prior to using the geo-replication features, Contoso had a US-based registry in West US, with an additional registry in West Europe.</span></span> <span data-ttu-id="349a3-122">To serve these different regions, the development team had to push images to two different registries.</span><span class="sxs-lookup"><span data-stu-id="349a3-122">To serve these different regions, the development team had to push images to two different registries.</span></span>

```bash
docker push contoso.azurecr.io/pubic/products/web:1.2
docker push contosowesteu.azurecr.io/pubic/products/web:1.2
```
<span data-ttu-id="349a3-123">![Pulling from multiple registries](media/container-registry-geo-replication/before-geo-replicate-pull.png)</span><span class="sxs-lookup"><span data-stu-id="349a3-123">![Pulling from multiple registries](media/container-registry-geo-replication/before-geo-replicate-pull.png)</span></span><br /><span data-ttu-id="349a3-124">*Pulling from multiple registries*</span><span class="sxs-lookup"><span data-stu-id="349a3-124">*Pulling from multiple registries*</span></span>

<span data-ttu-id="349a3-125">Typical challenges of multiple registries include:</span><span class="sxs-lookup"><span data-stu-id="349a3-125">Typical challenges of multiple registries include:</span></span>

* <span data-ttu-id="349a3-126">The East US, West US, and Canada Central clusters all pull from the West US registry, incurring egress fees as each of these remote container hosts pull images from West US data centers.</span><span class="sxs-lookup"><span data-stu-id="349a3-126">The East US, West US, and Canada Central clusters all pull from the West US registry, incurring egress fees as each of these remote container hosts pull images from West US data centers.</span></span>
* <span data-ttu-id="349a3-127">The development team must push images to West US and West Europe registries.</span><span class="sxs-lookup"><span data-stu-id="349a3-127">The development team must push images to West US and West Europe registries.</span></span>
* <span data-ttu-id="349a3-128">The development team must configure and maintain each regional deployment with image names referencing the local registry.</span><span class="sxs-lookup"><span data-stu-id="349a3-128">The development team must configure and maintain each regional deployment with image names referencing the local registry.</span></span>
* <span data-ttu-id="349a3-129">Registry access must be configured for each region.</span><span class="sxs-lookup"><span data-stu-id="349a3-129">Registry access must be configured for each region.</span></span>

## <a name="benefits-of-geo-replication"></a><span data-ttu-id="349a3-130">Benefits of geo-replication</span><span class="sxs-lookup"><span data-stu-id="349a3-130">Benefits of geo-replication</span></span>

![Pulling from a geo-replicated registry](media/container-registry-geo-replication/after-geo-replicate-pull.png)

<span data-ttu-id="349a3-132">Using the geo-replication feature of Azure Container Registry, these benefits are realized:</span><span class="sxs-lookup"><span data-stu-id="349a3-132">Using the geo-replication feature of Azure Container Registry, these benefits are realized:</span></span>

* <span data-ttu-id="349a3-133">Manage a single registry across all regions: `contoso.azurecr.io`</span><span class="sxs-lookup"><span data-stu-id="349a3-133">Manage a single registry across all regions: `contoso.azurecr.io`</span></span>
* <span data-ttu-id="349a3-134">Manage a single configuration of image deployments as all regions used the same image URL: `contoso.azurecr.io/public/products/web:1.2`</span><span class="sxs-lookup"><span data-stu-id="349a3-134">Manage a single configuration of image deployments as all regions used the same image URL: `contoso.azurecr.io/public/products/web:1.2`</span></span>
* <span data-ttu-id="349a3-135">Push to a single registry, while ACR manages the geo-replication, including regional webhooks for local notifications</span><span class="sxs-lookup"><span data-stu-id="349a3-135">Push to a single registry, while ACR manages the geo-replication, including regional webhooks for local notifications</span></span>

## <a name="configure-geo-replication"></a><span data-ttu-id="349a3-136">Configure geo-replication</span><span class="sxs-lookup"><span data-stu-id="349a3-136">Configure geo-replication</span></span>
<span data-ttu-id="349a3-137">Configuring geo-replication is as easy as clicking regions on a map.</span><span class="sxs-lookup"><span data-stu-id="349a3-137">Configuring geo-replication is as easy as clicking regions on a map.</span></span>

<span data-ttu-id="349a3-138">Geo-replication is a feature of [Premium registries](container-registry-skus.md) only.</span><span class="sxs-lookup"><span data-stu-id="349a3-138">Geo-replication is a feature of [Premium registries](container-registry-skus.md) only.</span></span> <span data-ttu-id="349a3-139">If your registry isn't yet Premium, you can change from Basic and Standard to Premium in the [Azure portal](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="349a3-139">If your registry isn't yet Premium, you can change from Basic and Standard to Premium in the [Azure portal](https://portal.azure.com):</span></span>

![Switching SKUs in the Azure portal](media/container-registry-skus/update-registry-sku.png)

<span data-ttu-id="349a3-141">To configure geo-replication for your Premium registry, log in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="349a3-141">To configure geo-replication for your Premium registry, log in to the Azure portal at http://portal.azure.com.</span></span>

<span data-ttu-id="349a3-142">Navigate to your Azure Container Registry, and select **Replications**:</span><span class="sxs-lookup"><span data-stu-id="349a3-142">Navigate to your Azure Container Registry, and select **Replications**:</span></span>

![Replications in the Azure portal container registry UI](media/container-registry-geo-replication/registry-services.png)

<span data-ttu-id="349a3-144">A map is displayed showing all current Azure Regions:</span><span class="sxs-lookup"><span data-stu-id="349a3-144">A map is displayed showing all current Azure Regions:</span></span>

 ![Region map in the Azure portal](media/container-registry-geo-replication/registry-geo-map.png)

* <span data-ttu-id="349a3-146">Blue hexagons represent current replicas</span><span class="sxs-lookup"><span data-stu-id="349a3-146">Blue hexagons represent current replicas</span></span>
* <span data-ttu-id="349a3-147">Green hexagons represent possible replica regions</span><span class="sxs-lookup"><span data-stu-id="349a3-147">Green hexagons represent possible replica regions</span></span>
* <span data-ttu-id="349a3-148">Gray hexagons represent Azure regions not yet available for replication</span><span class="sxs-lookup"><span data-stu-id="349a3-148">Gray hexagons represent Azure regions not yet available for replication</span></span>

<span data-ttu-id="349a3-149">To configure a replica, select a green hexagon, then select **Create**:</span><span class="sxs-lookup"><span data-stu-id="349a3-149">To configure a replica, select a green hexagon, then select **Create**:</span></span>

 ![Create replication UI in the Azure portal](media/container-registry-geo-replication/create-replication.png)

<span data-ttu-id="349a3-151">To configure additional replicas, select the green hexagons for other regions, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="349a3-151">To configure additional replicas, select the green hexagons for other regions, then click **Create**.</span></span>

<span data-ttu-id="349a3-152">ACR begins syncing images across the configured replicas.</span><span class="sxs-lookup"><span data-stu-id="349a3-152">ACR begins syncing images across the configured replicas.</span></span> <span data-ttu-id="349a3-153">Once complete, the portal reflects *Ready*.</span><span class="sxs-lookup"><span data-stu-id="349a3-153">Once complete, the portal reflects *Ready*.</span></span> <span data-ttu-id="349a3-154">The replica status in the portal doesn't automatically update.</span><span class="sxs-lookup"><span data-stu-id="349a3-154">The replica status in the portal doesn't automatically update.</span></span> <span data-ttu-id="349a3-155">Use the refresh button to see the updated status.</span><span class="sxs-lookup"><span data-stu-id="349a3-155">Use the refresh button to see the updated status.</span></span>

## <a name="geo-replication-pricing"></a><span data-ttu-id="349a3-156">Geo-replication pricing</span><span class="sxs-lookup"><span data-stu-id="349a3-156">Geo-replication pricing</span></span>

<span data-ttu-id="349a3-157">Geo-replication is a feature of the [Premium SKU](container-registry-skus.md) of Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="349a3-157">Geo-replication is a feature of the [Premium SKU](container-registry-skus.md) of Azure Container Registry.</span></span> <span data-ttu-id="349a3-158">When you replicate a registry to your desired regions, you incur Premium registry fees for each region.</span><span class="sxs-lookup"><span data-stu-id="349a3-158">When you replicate a registry to your desired regions, you incur Premium registry fees for each region.</span></span>

<span data-ttu-id="349a3-159">In the preceding example, Contoso consolidated two registries down to one, adding replicas to East US, Canada Central, and West Europe.</span><span class="sxs-lookup"><span data-stu-id="349a3-159">In the preceding example, Contoso consolidated two registries down to one, adding replicas to East US, Canada Central, and West Europe.</span></span> <span data-ttu-id="349a3-160">Contoso would pay four times Premium per month, with no additional configuration or management.</span><span class="sxs-lookup"><span data-stu-id="349a3-160">Contoso would pay four times Premium per month, with no additional configuration or management.</span></span> <span data-ttu-id="349a3-161">Each region now pulls their images locally, improving performance, reliability without network egress fees from West US to Canada and East US.</span><span class="sxs-lookup"><span data-stu-id="349a3-161">Each region now pulls their images locally, improving performance, reliability without network egress fees from West US to Canada and East US.</span></span>

## <a name="summary"></a><span data-ttu-id="349a3-162">Summary</span><span class="sxs-lookup"><span data-stu-id="349a3-162">Summary</span></span>

<span data-ttu-id="349a3-163">With geo-replication, you can manage your regional data centers as one global cloud.</span><span class="sxs-lookup"><span data-stu-id="349a3-163">With geo-replication, you can manage your regional data centers as one global cloud.</span></span> <span data-ttu-id="349a3-164">As images are used across many Azure services, you can benefit from a single management plane while maintaining network-close, fast, and reliable local image pulls.</span><span class="sxs-lookup"><span data-stu-id="349a3-164">As images are used across many Azure services, you can benefit from a single management plane while maintaining network-close, fast, and reliable local image pulls.</span></span>

## <a name="next-steps"></a><span data-ttu-id="349a3-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="349a3-165">Next steps</span></span>

<span data-ttu-id="349a3-166">Check out the three-part tutorial series, [Geo-replication in Azure Container Registry](container-registry-tutorial-prepare-registry.md).</span><span class="sxs-lookup"><span data-stu-id="349a3-166">Check out the three-part tutorial series, [Geo-replication in Azure Container Registry](container-registry-tutorial-prepare-registry.md).</span></span> <span data-ttu-id="349a3-167">Walk through creating a geo-replicated registry, building a container, and then deploying it with a single `docker push` command to multiple regional Web Apps for Containers instances.</span><span class="sxs-lookup"><span data-stu-id="349a3-167">Walk through creating a geo-replicated registry, building a container, and then deploying it with a single `docker push` command to multiple regional Web Apps for Containers instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="349a3-168">Geo-replication in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="349a3-168">Geo-replication in Azure Container Registry</span></span>](container-registry-tutorial-prepare-registry.md)