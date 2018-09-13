---
title: Best practices in Azure Container Registry
description: Learn how to use your Azure container registry effectively by following these best practices.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: quickstart
ms.date: 04/10/2018
ms.author: marsma
ms.openlocfilehash: a3932ff621782b8ab97f27ef052aeee8e1d2a3ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856734"
---
# <a name="best-practices-for-azure-container-registry"></a><span data-ttu-id="b6c22-103">Best practices for Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="b6c22-103">Best practices for Azure Container Registry</span></span>

<span data-ttu-id="b6c22-104">By following these best practices, you can help maximize the performance and cost-effective use of your private Docker registry in Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c22-104">By following these best practices, you can help maximize the performance and cost-effective use of your private Docker registry in Azure.</span></span>

## <a name="network-close-deployment"></a><span data-ttu-id="b6c22-105">Network-close deployment</span><span class="sxs-lookup"><span data-stu-id="b6c22-105">Network-close deployment</span></span>

<span data-ttu-id="b6c22-106">Create your container registry in the same Azure region in which you deploy containers.</span><span class="sxs-lookup"><span data-stu-id="b6c22-106">Create your container registry in the same Azure region in which you deploy containers.</span></span> <span data-ttu-id="b6c22-107">Placing your registry in a region that is network-close to your container hosts can help lower both latency and cost.</span><span class="sxs-lookup"><span data-stu-id="b6c22-107">Placing your registry in a region that is network-close to your container hosts can help lower both latency and cost.</span></span>

<span data-ttu-id="b6c22-108">Network-close deployment is one of the primary reasons for using a private container registry.</span><span class="sxs-lookup"><span data-stu-id="b6c22-108">Network-close deployment is one of the primary reasons for using a private container registry.</span></span> <span data-ttu-id="b6c22-109">Docker images have an efficient [layering construct](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/) that allows for incremental deployments.</span><span class="sxs-lookup"><span data-stu-id="b6c22-109">Docker images have an efficient [layering construct](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/) that allows for incremental deployments.</span></span> <span data-ttu-id="b6c22-110">However, new nodes need to pull all layers required for a given image.</span><span class="sxs-lookup"><span data-stu-id="b6c22-110">However, new nodes need to pull all layers required for a given image.</span></span> <span data-ttu-id="b6c22-111">This initial `docker pull` can quickly add up to multiple gigabytes.</span><span class="sxs-lookup"><span data-stu-id="b6c22-111">This initial `docker pull` can quickly add up to multiple gigabytes.</span></span> <span data-ttu-id="b6c22-112">Having a private registry close to your deployment minimizes the network latency.</span><span class="sxs-lookup"><span data-stu-id="b6c22-112">Having a private registry close to your deployment minimizes the network latency.</span></span>
<span data-ttu-id="b6c22-113">Additionally, all public clouds, Azure included, implement network egress fees.</span><span class="sxs-lookup"><span data-stu-id="b6c22-113">Additionally, all public clouds, Azure included, implement network egress fees.</span></span> <span data-ttu-id="b6c22-114">Pulling images from one datacenter to another adds network egress fees, in addition to the latency.</span><span class="sxs-lookup"><span data-stu-id="b6c22-114">Pulling images from one datacenter to another adds network egress fees, in addition to the latency.</span></span>

## <a name="geo-replicate-multi-region-deployments"></a><span data-ttu-id="b6c22-115">Geo-replicate multi-region deployments</span><span class="sxs-lookup"><span data-stu-id="b6c22-115">Geo-replicate multi-region deployments</span></span>

<span data-ttu-id="b6c22-116">Use Azure Container Registry's [geo-replication](container-registry-geo-replication.md) feature if you're deploying containers to multiple regions.</span><span class="sxs-lookup"><span data-stu-id="b6c22-116">Use Azure Container Registry's [geo-replication](container-registry-geo-replication.md) feature if you're deploying containers to multiple regions.</span></span> <span data-ttu-id="b6c22-117">Whether you're serving global customers from local data centers or your development team is in different locations, you can simplify registry management and minimize latency by geo-replicating your registry.</span><span class="sxs-lookup"><span data-stu-id="b6c22-117">Whether you're serving global customers from local data centers or your development team is in different locations, you can simplify registry management and minimize latency by geo-replicating your registry.</span></span> <span data-ttu-id="b6c22-118">Geo-replication is available only with [Premium](container-registry-skus.md) registries.</span><span class="sxs-lookup"><span data-stu-id="b6c22-118">Geo-replication is available only with [Premium](container-registry-skus.md) registries.</span></span>

<span data-ttu-id="b6c22-119">To learn how to use geo-replication, see the three-part tutorial, [Geo-replication in Azure Container Registry](container-registry-tutorial-prepare-registry.md).</span><span class="sxs-lookup"><span data-stu-id="b6c22-119">To learn how to use geo-replication, see the three-part tutorial, [Geo-replication in Azure Container Registry](container-registry-tutorial-prepare-registry.md).</span></span>

## <a name="repository-namespaces"></a><span data-ttu-id="b6c22-120">Repository namespaces</span><span class="sxs-lookup"><span data-stu-id="b6c22-120">Repository namespaces</span></span>

<span data-ttu-id="b6c22-121">By leveraging repository namespaces, you can allow sharing a single registry across multiple groups within your organization.</span><span class="sxs-lookup"><span data-stu-id="b6c22-121">By leveraging repository namespaces, you can allow sharing a single registry across multiple groups within your organization.</span></span> <span data-ttu-id="b6c22-122">Registries can be shared across deployments and teams.</span><span class="sxs-lookup"><span data-stu-id="b6c22-122">Registries can be shared across deployments and teams.</span></span> <span data-ttu-id="b6c22-123">Azure Container Registry supports nested namespaces, enabling group isolation.</span><span class="sxs-lookup"><span data-stu-id="b6c22-123">Azure Container Registry supports nested namespaces, enabling group isolation.</span></span>

<span data-ttu-id="b6c22-124">For example, consider the following container image tags.</span><span class="sxs-lookup"><span data-stu-id="b6c22-124">For example, consider the following container image tags.</span></span> <span data-ttu-id="b6c22-125">Images that are used corporate-wide, like `aspnetcore`, are placed in the root namespace, while container images owned by the Production and Marketing groups each use their own namespaces.</span><span class="sxs-lookup"><span data-stu-id="b6c22-125">Images that are used corporate-wide, like `aspnetcore`, are placed in the root namespace, while container images owned by the Production and Marketing groups each use their own namespaces.</span></span>

```
contoso.azurecr.io/aspnetcore:2.0
contoso.azurecr.io/products/widget/web:1
contoso.azurecr.io/products/bettermousetrap/refundapi:12.3
contoso.azurecr.io/marketing/2017-fall/concertpromotions/campaign:218.42
```

## <a name="dedicated-resource-group"></a><span data-ttu-id="b6c22-126">Dedicated resource group</span><span class="sxs-lookup"><span data-stu-id="b6c22-126">Dedicated resource group</span></span>

<span data-ttu-id="b6c22-127">Because container registries are resources that are used across multiple container hosts, a registry should reside its own resource group.</span><span class="sxs-lookup"><span data-stu-id="b6c22-127">Because container registries are resources that are used across multiple container hosts, a registry should reside its own resource group.</span></span>

<span data-ttu-id="b6c22-128">Although you might experiment with a specific host type, such as Azure Container Instances, you'll likely want to delete the container instance when you're done.</span><span class="sxs-lookup"><span data-stu-id="b6c22-128">Although you might experiment with a specific host type, such as Azure Container Instances, you'll likely want to delete the container instance when you're done.</span></span> <span data-ttu-id="b6c22-129">However, you might also want to keep the collection of images you pushed to Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="b6c22-129">However, you might also want to keep the collection of images you pushed to Azure Container Registry.</span></span> <span data-ttu-id="b6c22-130">By placing your registry in its own resource group, you minimize the risk of accidentally deleting the collection of images in the registry when you delete the container instance resource group.</span><span class="sxs-lookup"><span data-stu-id="b6c22-130">By placing your registry in its own resource group, you minimize the risk of accidentally deleting the collection of images in the registry when you delete the container instance resource group.</span></span>

## <a name="authentication"></a><span data-ttu-id="b6c22-131">Authentication</span><span class="sxs-lookup"><span data-stu-id="b6c22-131">Authentication</span></span>

<span data-ttu-id="b6c22-132">When authenticating with an Azure container registry, there are two primary scenarios: individual authentication, and service (or "headless") authentication.</span><span class="sxs-lookup"><span data-stu-id="b6c22-132">When authenticating with an Azure container registry, there are two primary scenarios: individual authentication, and service (or "headless") authentication.</span></span> <span data-ttu-id="b6c22-133">The following table provides a brief overview of these scenarios, and the recommended method of authentication for each.</span><span class="sxs-lookup"><span data-stu-id="b6c22-133">The following table provides a brief overview of these scenarios, and the recommended method of authentication for each.</span></span>

| <span data-ttu-id="b6c22-134">Type</span><span class="sxs-lookup"><span data-stu-id="b6c22-134">Type</span></span> | <span data-ttu-id="b6c22-135">Example scenario</span><span class="sxs-lookup"><span data-stu-id="b6c22-135">Example scenario</span></span> | <span data-ttu-id="b6c22-136">Recommended method</span><span class="sxs-lookup"><span data-stu-id="b6c22-136">Recommended method</span></span> |
|---|---|---|
| <span data-ttu-id="b6c22-137">Individual identity</span><span class="sxs-lookup"><span data-stu-id="b6c22-137">Individual identity</span></span> | <span data-ttu-id="b6c22-138">A developer pulling images to or pushing images from their development machine.</span><span class="sxs-lookup"><span data-stu-id="b6c22-138">A developer pulling images to or pushing images from their development machine.</span></span> | [<span data-ttu-id="b6c22-139">az acr login</span><span class="sxs-lookup"><span data-stu-id="b6c22-139">az acr login</span></span>](/cli/azure/acr?view=azure-cli-latest#az-acr-login) |
| <span data-ttu-id="b6c22-140">Headless/service identity</span><span class="sxs-lookup"><span data-stu-id="b6c22-140">Headless/service identity</span></span> | <span data-ttu-id="b6c22-141">Build and deployment pipelines where the user isn't directly involved.</span><span class="sxs-lookup"><span data-stu-id="b6c22-141">Build and deployment pipelines where the user isn't directly involved.</span></span> | [<span data-ttu-id="b6c22-142">Service principal</span><span class="sxs-lookup"><span data-stu-id="b6c22-142">Service principal</span></span>](container-registry-authentication.md#service-principal) |

<span data-ttu-id="b6c22-143">For in-depth information about Azure Container Registry authentication, see [Authenticate with an Azure container registry](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b6c22-143">For in-depth information about Azure Container Registry authentication, see [Authenticate with an Azure container registry](container-registry-authentication.md).</span></span>

## <a name="manage-registry-size"></a><span data-ttu-id="b6c22-144">Manage registry size</span><span class="sxs-lookup"><span data-stu-id="b6c22-144">Manage registry size</span></span>

<span data-ttu-id="b6c22-145">The storage constraints of each [container registry SKU][container-registry-skus] are intended to align with a typical scenario: **Basic** for getting started, **Standard** for the majority of production applications, and **Premium** for hyper-scale performance and [geo-replication][container-registry-geo-replication].</span><span class="sxs-lookup"><span data-stu-id="b6c22-145">The storage constraints of each [container registry SKU][container-registry-skus] are intended to align with a typical scenario: **Basic** for getting started, **Standard** for the majority of production applications, and **Premium** for hyper-scale performance and [geo-replication][container-registry-geo-replication].</span></span> <span data-ttu-id="b6c22-146">Throughout the life of your registry, you should manage its size by periodically deleting unused content.</span><span class="sxs-lookup"><span data-stu-id="b6c22-146">Throughout the life of your registry, you should manage its size by periodically deleting unused content.</span></span>

<span data-ttu-id="b6c22-147">You can find the current usage of a registry in the container registry **Overview** in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="b6c22-147">You can find the current usage of a registry in the container registry **Overview** in the Azure portal:</span></span>

![Registry usage information in the Azure portal][registry-overview-quotas]

<span data-ttu-id="b6c22-149">You can manage the size of your registry by using the [Azure CLI][azure-cli] or the [Azure portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b6c22-149">You can manage the size of your registry by using the [Azure CLI][azure-cli] or the [Azure portal][azure-portal].</span></span> <span data-ttu-id="b6c22-150">Only the managed SKUs (Basic, Standard, Premium) support repository and image deletion--you cannot delete repositories, images, or tags in a Classic registry.</span><span class="sxs-lookup"><span data-stu-id="b6c22-150">Only the managed SKUs (Basic, Standard, Premium) support repository and image deletion--you cannot delete repositories, images, or tags in a Classic registry.</span></span>

### <a name="delete-in-azure-cli"></a><span data-ttu-id="b6c22-151">Delete in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b6c22-151">Delete in Azure CLI</span></span>

<span data-ttu-id="b6c22-152">Use the [az acr repository delete][az-acr-repository-delete] command to delete a repository, or content within a repository.</span><span class="sxs-lookup"><span data-stu-id="b6c22-152">Use the [az acr repository delete][az-acr-repository-delete] command to delete a repository, or content within a repository.</span></span>

<span data-ttu-id="b6c22-153">To delete a repository, including all tags and image layer data within the repository, specify only the repository name when you execute [az acr repository delete][az-acr-repository-delete].</span><span class="sxs-lookup"><span data-stu-id="b6c22-153">To delete a repository, including all tags and image layer data within the repository, specify only the repository name when you execute [az acr repository delete][az-acr-repository-delete].</span></span> <span data-ttu-id="b6c22-154">In the following example, we delete the *myapplication* repository, and all tags and image layer data within the repository:</span><span class="sxs-lookup"><span data-stu-id="b6c22-154">In the following example, we delete the *myapplication* repository, and all tags and image layer data within the repository:</span></span>

```azurecli
az acr repository delete --name myregistry --repository myapplication
```

<span data-ttu-id="b6c22-155">You can also delete image data from a repository by using the `--tag` and `--manifest` arguments.</span><span class="sxs-lookup"><span data-stu-id="b6c22-155">You can also delete image data from a repository by using the `--tag` and `--manifest` arguments.</span></span> <span data-ttu-id="b6c22-156">For details on these arguments, see the [az acr repository delete command reference][az-acr-repository-delete].</span><span class="sxs-lookup"><span data-stu-id="b6c22-156">For details on these arguments, see the [az acr repository delete command reference][az-acr-repository-delete].</span></span>

### <a name="delete-in-azure-portal"></a><span data-ttu-id="b6c22-157">Delete in Azure portal</span><span class="sxs-lookup"><span data-stu-id="b6c22-157">Delete in Azure portal</span></span>

<span data-ttu-id="b6c22-158">To delete a repository from a registry in the Azure portal, first navigate to your container registry.</span><span class="sxs-lookup"><span data-stu-id="b6c22-158">To delete a repository from a registry in the Azure portal, first navigate to your container registry.</span></span> <span data-ttu-id="b6c22-159">Then, under **SERVICES**, select **Repositories**, and right-click the repository you want to delete.</span><span class="sxs-lookup"><span data-stu-id="b6c22-159">Then, under **SERVICES**, select **Repositories**, and right-click the repository you want to delete.</span></span> <span data-ttu-id="b6c22-160">Select **Delete** to delete the repository and the Docker images it contains.</span><span class="sxs-lookup"><span data-stu-id="b6c22-160">Select **Delete** to delete the repository and the Docker images it contains.</span></span>

![Delete a repository in the Azure portal][delete-repository-portal]

<span data-ttu-id="b6c22-162">In a similar manner, you can also delete tags from a repository.</span><span class="sxs-lookup"><span data-stu-id="b6c22-162">In a similar manner, you can also delete tags from a repository.</span></span> <span data-ttu-id="b6c22-163">Navigate to the repository, right-click on the tag you wish to delete under **TAGS**, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b6c22-163">Navigate to the repository, right-click on the tag you wish to delete under **TAGS**, and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6c22-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6c22-164">Next steps</span></span>

<span data-ttu-id="b6c22-165">Azure Container Registry is available in several tiers, called SKUs, that each provide different capabilities.</span><span class="sxs-lookup"><span data-stu-id="b6c22-165">Azure Container Registry is available in several tiers, called SKUs, that each provide different capabilities.</span></span> <span data-ttu-id="b6c22-166">For details on the available SKUs, see [Azure Container Registry SKUs](container-registry-skus.md).</span><span class="sxs-lookup"><span data-stu-id="b6c22-166">For details on the available SKUs, see [Azure Container Registry SKUs](container-registry-skus.md).</span></span>

<!-- IMAGES -->
[delete-repository-portal]: ./media/container-registry-best-practices/delete-repository-portal.png
[registry-overview-quotas]: ./media/container-registry-best-practices/registry-overview-quotas.png

<!-- LINKS - Internal -->
[az-acr-repository-delete]: /cli/azure/acr/repository#az-acr-repository-delete
[azure-cli]: /cli/azure
[azure-portal]: https://portal.azure.com
[container-registry-geo-replication]: container-registry-geo-replication.md
[container-registry-skus]: container-registry-skus.md
