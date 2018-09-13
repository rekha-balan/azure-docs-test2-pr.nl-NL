---
title: Azure Container Registry SKUs
description: Compare the different service tiers available in Azure Container Registry.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 08/30/2018
ms.author: marsma
ms.openlocfilehash: eb3a1745677871211df05d18e28d32061f360bac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868345"
---
# <a name="azure-container-registry-skus"></a><span data-ttu-id="05d07-103">Azure Container Registry SKUs</span><span class="sxs-lookup"><span data-stu-id="05d07-103">Azure Container Registry SKUs</span></span>

<span data-ttu-id="05d07-104">Azure Container Registry (ACR) is available in multiple service tiers, known as SKUs.</span><span class="sxs-lookup"><span data-stu-id="05d07-104">Azure Container Registry (ACR) is available in multiple service tiers, known as SKUs.</span></span> <span data-ttu-id="05d07-105">These SKUs provide predictable pricing and several options for aligning to the capacity and usage patterns of your private Docker registry in Azure.</span><span class="sxs-lookup"><span data-stu-id="05d07-105">These SKUs provide predictable pricing and several options for aligning to the capacity and usage patterns of your private Docker registry in Azure.</span></span>

| <span data-ttu-id="05d07-106">SKU</span><span class="sxs-lookup"><span data-stu-id="05d07-106">SKU</span></span> | <span data-ttu-id="05d07-107">Managed</span><span class="sxs-lookup"><span data-stu-id="05d07-107">Managed</span></span> | <span data-ttu-id="05d07-108">Description</span><span class="sxs-lookup"><span data-stu-id="05d07-108">Description</span></span> |
| --- | :-------: | ----------- |
| <span data-ttu-id="05d07-109">**Basic**</span><span class="sxs-lookup"><span data-stu-id="05d07-109">**Basic**</span></span> | <span data-ttu-id="05d07-110">Yes</span><span class="sxs-lookup"><span data-stu-id="05d07-110">Yes</span></span> | <span data-ttu-id="05d07-111">A cost-optimized entry point for developers learning about Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="05d07-111">A cost-optimized entry point for developers learning about Azure Container Registry.</span></span> <span data-ttu-id="05d07-112">Basic registries have the same programmatic capabilities as Standard and Premium (Azure Active Directory authentication integration, image deletion, and web hooks).</span><span class="sxs-lookup"><span data-stu-id="05d07-112">Basic registries have the same programmatic capabilities as Standard and Premium (Azure Active Directory authentication integration, image deletion, and web hooks).</span></span> <span data-ttu-id="05d07-113">However, the included storage and image throughput are most appropriate for lower usage scenarios.</span><span class="sxs-lookup"><span data-stu-id="05d07-113">However, the included storage and image throughput are most appropriate for lower usage scenarios.</span></span> |
| <span data-ttu-id="05d07-114">**Standard**</span><span class="sxs-lookup"><span data-stu-id="05d07-114">**Standard**</span></span> | <span data-ttu-id="05d07-115">Yes</span><span class="sxs-lookup"><span data-stu-id="05d07-115">Yes</span></span> | <span data-ttu-id="05d07-116">Standard registries offer the same capabilities as Basic, with increased included storage and image throughput.</span><span class="sxs-lookup"><span data-stu-id="05d07-116">Standard registries offer the same capabilities as Basic, with increased included storage and image throughput.</span></span> <span data-ttu-id="05d07-117">Standard registries should satisfy the needs of most production scenarios.</span><span class="sxs-lookup"><span data-stu-id="05d07-117">Standard registries should satisfy the needs of most production scenarios.</span></span> |
| <span data-ttu-id="05d07-118">**Premium**</span><span class="sxs-lookup"><span data-stu-id="05d07-118">**Premium**</span></span> | <span data-ttu-id="05d07-119">Yes</span><span class="sxs-lookup"><span data-stu-id="05d07-119">Yes</span></span> | <span data-ttu-id="05d07-120">Premium registries provide the highest amount of included storage and concurrent operations, enabling high-volume scenarios.</span><span class="sxs-lookup"><span data-stu-id="05d07-120">Premium registries provide the highest amount of included storage and concurrent operations, enabling high-volume scenarios.</span></span> <span data-ttu-id="05d07-121">In addition to higher image throughput, Premium adds features like [geo-replication][container-registry-geo-replication] for managing a single registry across multiple regions, and [content trust (preview)](container-registry-content-trust.md) for image tag signing.</span><span class="sxs-lookup"><span data-stu-id="05d07-121">In addition to higher image throughput, Premium adds features like [geo-replication][container-registry-geo-replication] for managing a single registry across multiple regions, and [content trust (preview)](container-registry-content-trust.md) for image tag signing.</span></span> |
| <span data-ttu-id="05d07-122">Classic<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="05d07-122">Classic<sup>1</sup></span></span> | <span data-ttu-id="05d07-123">No</span><span class="sxs-lookup"><span data-stu-id="05d07-123">No</span></span> | <span data-ttu-id="05d07-124">This SKU enabled the initial release of the Azure Container Registry service in Azure.</span><span class="sxs-lookup"><span data-stu-id="05d07-124">This SKU enabled the initial release of the Azure Container Registry service in Azure.</span></span> <span data-ttu-id="05d07-125">Classic registries are backed by a storage account that Azure creates in your subscription, which limits the ability for ACR to provide higher-level capabilities such as increased throughput and geo-replication.</span><span class="sxs-lookup"><span data-stu-id="05d07-125">Classic registries are backed by a storage account that Azure creates in your subscription, which limits the ability for ACR to provide higher-level capabilities such as increased throughput and geo-replication.</span></span> |

<span data-ttu-id="05d07-126"><sup>1</sup> The Classic SKU will be **deprecated** in **March 2019**.</span><span class="sxs-lookup"><span data-stu-id="05d07-126"><sup>1</sup> The Classic SKU will be **deprecated** in **March 2019**.</span></span> <span data-ttu-id="05d07-127">Use Basic, Standard, or Premium for all new container registries.</span><span class="sxs-lookup"><span data-stu-id="05d07-127">Use Basic, Standard, or Premium for all new container registries.</span></span>

<span data-ttu-id="05d07-128">Choosing a higher-level SKU provides more performance and scale, however, all managed SKUs provide the same programmatic capabilities.</span><span class="sxs-lookup"><span data-stu-id="05d07-128">Choosing a higher-level SKU provides more performance and scale, however, all managed SKUs provide the same programmatic capabilities.</span></span> <span data-ttu-id="05d07-129">With multiple service tiers, you can get started with Basic, then convert to Standard and Premium as your registry usage increases.</span><span class="sxs-lookup"><span data-stu-id="05d07-129">With multiple service tiers, you can get started with Basic, then convert to Standard and Premium as your registry usage increases.</span></span>

## <a name="managed-vs-unmanaged"></a><span data-ttu-id="05d07-130">Managed vs. unmanaged</span><span class="sxs-lookup"><span data-stu-id="05d07-130">Managed vs. unmanaged</span></span>

<span data-ttu-id="05d07-131">The Basic, Standard, and Premium SKUs are collectively known as *managed* registries, and Classic registries as *unmanaged*.</span><span class="sxs-lookup"><span data-stu-id="05d07-131">The Basic, Standard, and Premium SKUs are collectively known as *managed* registries, and Classic registries as *unmanaged*.</span></span> <span data-ttu-id="05d07-132">The primary difference between the two is how your container images are stored.</span><span class="sxs-lookup"><span data-stu-id="05d07-132">The primary difference between the two is how your container images are stored.</span></span>

### <a name="managed-basic-standard-premium"></a><span data-ttu-id="05d07-133">Managed (Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="05d07-133">Managed (Basic, Standard, Premium)</span></span>

<span data-ttu-id="05d07-134">Managed registries benefit from image storage managed entirely by Azure.</span><span class="sxs-lookup"><span data-stu-id="05d07-134">Managed registries benefit from image storage managed entirely by Azure.</span></span> <span data-ttu-id="05d07-135">That is, a storage account that stores your images does not appear within your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="05d07-135">That is, a storage account that stores your images does not appear within your Azure subscription.</span></span> <span data-ttu-id="05d07-136">There are several benefits gained by using one of the managed registry SKUs, discussed in-depth in [Container image storage in Azure Container Registry][container-registry-storage].</span><span class="sxs-lookup"><span data-stu-id="05d07-136">There are several benefits gained by using one of the managed registry SKUs, discussed in-depth in [Container image storage in Azure Container Registry][container-registry-storage].</span></span> <span data-ttu-id="05d07-137">This article focuses on the managed registry SKUs and their capabilities.</span><span class="sxs-lookup"><span data-stu-id="05d07-137">This article focuses on the managed registry SKUs and their capabilities.</span></span>

### <a name="unmanaged-classic"></a><span data-ttu-id="05d07-138">Unmanaged (Classic)</span><span class="sxs-lookup"><span data-stu-id="05d07-138">Unmanaged (Classic)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05d07-139">The Classic SKU is being deprecated, and will be unavailable after March 2019.</span><span class="sxs-lookup"><span data-stu-id="05d07-139">The Classic SKU is being deprecated, and will be unavailable after March 2019.</span></span> <span data-ttu-id="05d07-140">Use Basic, Standard, or Premium for all new registries.</span><span class="sxs-lookup"><span data-stu-id="05d07-140">Use Basic, Standard, or Premium for all new registries.</span></span>

<span data-ttu-id="05d07-141">Classic registries are "unmanaged" in the sense that the storage account that backs a Classic registry resides within *your* Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="05d07-141">Classic registries are "unmanaged" in the sense that the storage account that backs a Classic registry resides within *your* Azure subscription.</span></span> <span data-ttu-id="05d07-142">As such, you are responsible for the management of the storage account in which your container images are stored.</span><span class="sxs-lookup"><span data-stu-id="05d07-142">As such, you are responsible for the management of the storage account in which your container images are stored.</span></span> <span data-ttu-id="05d07-143">With unmanaged registries, you can't switch between SKUs as your needs change (other than [upgrading][container-registry-upgrade] to a managed registry), and several features of managed registries are unavailable (for example, container image deletion, [geo-replication][container-registry-geo-replication], and [webhooks][container-registry-webhook]).</span><span class="sxs-lookup"><span data-stu-id="05d07-143">With unmanaged registries, you can't switch between SKUs as your needs change (other than [upgrading][container-registry-upgrade] to a managed registry), and several features of managed registries are unavailable (for example, container image deletion, [geo-replication][container-registry-geo-replication], and [webhooks][container-registry-webhook]).</span></span>

<span data-ttu-id="05d07-144">For more information about upgrading a Classic registry to one of the managed SKUs, see [Upgrade a Classic registry][container-registry-upgrade].</span><span class="sxs-lookup"><span data-stu-id="05d07-144">For more information about upgrading a Classic registry to one of the managed SKUs, see [Upgrade a Classic registry][container-registry-upgrade].</span></span>

## <a name="sku-feature-matrix"></a><span data-ttu-id="05d07-145">SKU feature matrix</span><span class="sxs-lookup"><span data-stu-id="05d07-145">SKU feature matrix</span></span>

<span data-ttu-id="05d07-146">The following table details the features and limits of the Basic, Standard, and Premium service tiers.</span><span class="sxs-lookup"><span data-stu-id="05d07-146">The following table details the features and limits of the Basic, Standard, and Premium service tiers.</span></span>

[!INCLUDE [container-instances-limits](../../includes/container-registry-limits.md)]

## <a name="changing-skus"></a><span data-ttu-id="05d07-147">Changing SKUs</span><span class="sxs-lookup"><span data-stu-id="05d07-147">Changing SKUs</span></span>

<span data-ttu-id="05d07-148">You can change a registry's SKU with the Azure CLI or in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05d07-148">You can change a registry's SKU with the Azure CLI or in the Azure portal.</span></span> <span data-ttu-id="05d07-149">You can move freely between managed SKUs as long as the SKU you're switching to has the required maximum storage capacity.</span><span class="sxs-lookup"><span data-stu-id="05d07-149">You can move freely between managed SKUs as long as the SKU you're switching to has the required maximum storage capacity.</span></span> <span data-ttu-id="05d07-150">If you switch to one of the managed SKUs from Classic, you cannot move back to Classic--it is a one-way conversion.</span><span class="sxs-lookup"><span data-stu-id="05d07-150">If you switch to one of the managed SKUs from Classic, you cannot move back to Classic--it is a one-way conversion.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="05d07-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="05d07-151">Azure CLI</span></span>

<span data-ttu-id="05d07-152">To move between SKUs in the Azure CLI, use the [az acr update][az-acr-update] command.</span><span class="sxs-lookup"><span data-stu-id="05d07-152">To move between SKUs in the Azure CLI, use the [az acr update][az-acr-update] command.</span></span> <span data-ttu-id="05d07-153">For example, to switch to Premium:</span><span class="sxs-lookup"><span data-stu-id="05d07-153">For example, to switch to Premium:</span></span>

```azurecli
az acr update --name myregistry --sku Premium
```

### <a name="azure-portal"></a><span data-ttu-id="05d07-154">Azure portal</span><span class="sxs-lookup"><span data-stu-id="05d07-154">Azure portal</span></span>

<span data-ttu-id="05d07-155">In the container registry **Overview** in the Azure portal, select **Update**, then select a new **SKU** from the SKU drop-down.</span><span class="sxs-lookup"><span data-stu-id="05d07-155">In the container registry **Overview** in the Azure portal, select **Update**, then select a new **SKU** from the SKU drop-down.</span></span>

![Update container registry SKU in Azure portal][update-registry-sku]

<span data-ttu-id="05d07-157">If you have a Classic registry, you can't select a managed SKU within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="05d07-157">If you have a Classic registry, you can't select a managed SKU within the Azure portal.</span></span> <span data-ttu-id="05d07-158">Instead, you must first [upgrade][container-registry-upgrade] to a managed registry (see [Changing from Classic](#changing-from-classic)).</span><span class="sxs-lookup"><span data-stu-id="05d07-158">Instead, you must first [upgrade][container-registry-upgrade] to a managed registry (see [Changing from Classic](#changing-from-classic)).</span></span>

## <a name="changing-from-classic"></a><span data-ttu-id="05d07-159">Changing from Classic</span><span class="sxs-lookup"><span data-stu-id="05d07-159">Changing from Classic</span></span>

<span data-ttu-id="05d07-160">There are additional considerations to take into account when migrating an unmanaged Classic registry to one of the managed Basic, Standard, or Premium SKUs.</span><span class="sxs-lookup"><span data-stu-id="05d07-160">There are additional considerations to take into account when migrating an unmanaged Classic registry to one of the managed Basic, Standard, or Premium SKUs.</span></span> <span data-ttu-id="05d07-161">If your Classic registry contains a large number of images and is many gigabytes in size, the migration process can take some time.</span><span class="sxs-lookup"><span data-stu-id="05d07-161">If your Classic registry contains a large number of images and is many gigabytes in size, the migration process can take some time.</span></span> <span data-ttu-id="05d07-162">Additionally, `docker push` operations are disabled until the migration is complete.</span><span class="sxs-lookup"><span data-stu-id="05d07-162">Additionally, `docker push` operations are disabled until the migration is complete.</span></span>

<span data-ttu-id="05d07-163">For details on upgrading your Classic registry to one of the managed SKUs, see [Upgrade a Classic container registry][container-registry-upgrade].</span><span class="sxs-lookup"><span data-stu-id="05d07-163">For details on upgrading your Classic registry to one of the managed SKUs, see [Upgrade a Classic container registry][container-registry-upgrade].</span></span>

## <a name="pricing"></a><span data-ttu-id="05d07-164">Pricing</span><span class="sxs-lookup"><span data-stu-id="05d07-164">Pricing</span></span>

<span data-ttu-id="05d07-165">For pricing information on each of the Azure Container Registry SKUs, see [Container Registry pricing][container-registry-pricing].</span><span class="sxs-lookup"><span data-stu-id="05d07-165">For pricing information on each of the Azure Container Registry SKUs, see [Container Registry pricing][container-registry-pricing].</span></span>

## <a name="next-steps"></a><span data-ttu-id="05d07-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="05d07-166">Next steps</span></span>

<span data-ttu-id="05d07-167">**Azure Container Registry Roadmap**</span><span class="sxs-lookup"><span data-stu-id="05d07-167">**Azure Container Registry Roadmap**</span></span>

<span data-ttu-id="05d07-168">Visit the [ACR Roadmap][acr-roadmap] on GitHub to find information about upcoming features in the service.</span><span class="sxs-lookup"><span data-stu-id="05d07-168">Visit the [ACR Roadmap][acr-roadmap] on GitHub to find information about upcoming features in the service.</span></span>

<span data-ttu-id="05d07-169">**Azure Container Registry UserVoice**</span><span class="sxs-lookup"><span data-stu-id="05d07-169">**Azure Container Registry UserVoice**</span></span>

<span data-ttu-id="05d07-170">Submit and vote on new feature suggestions in [ACR UserVoice][container-registry-uservoice].</span><span class="sxs-lookup"><span data-stu-id="05d07-170">Submit and vote on new feature suggestions in [ACR UserVoice][container-registry-uservoice].</span></span>

<!-- IMAGES -->
[update-registry-sku]: ./media/container-registry-skus/update-registry-sku.png

<!-- LINKS - External -->
[acr-roadmap]: https://aka.ms/acr/roadmap
[container-registry-pricing]: https://azure.microsoft.com/pricing/details/container-registry/
[container-registry-uservoice]: https://feedback.azure.com/forums/903958-azure-container-registry

<!-- LINKS - Internal -->
[az-acr-update]: /cli/azure/acr#az-acr-update
[container-registry-geo-replication]: container-registry-geo-replication.md
[container-registry-upgrade]: container-registry-upgrade.md
[container-registry-storage]: container-registry-storage.md
[container-registry-webhook]: container-registry-webhook.md
