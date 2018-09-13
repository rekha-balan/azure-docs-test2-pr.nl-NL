---
title: Upgrade a Classic Azure container registry
description: Take advantage of the expanded feature set of Basic, Standard, and Premium managed container registries by upgrading your unmanaged Classic container registry.
services: container-registry
author: mmacy
ms.service: container-registry
ms.topic: article
ms.date: 08/28/2018
ms.author: marsma
ms.openlocfilehash: 951866c1c74cb14536ea341d80c06e0fcfe0e4fe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867675"
---
# <a name="upgrade-a-classic-container-registry"></a><span data-ttu-id="5efed-103">Upgrade a Classic container registry</span><span class="sxs-lookup"><span data-stu-id="5efed-103">Upgrade a Classic container registry</span></span>

<span data-ttu-id="5efed-104">Azure Container Registry (ACR) is available in several service tiers, [known as SKUs](container-registry-skus.md).</span><span class="sxs-lookup"><span data-stu-id="5efed-104">Azure Container Registry (ACR) is available in several service tiers, [known as SKUs](container-registry-skus.md).</span></span> <span data-ttu-id="5efed-105">The initial release of ACR offered a single SKU, Classic, that lacks several features inherent to the Basic, Standard, and Premium SKUs (collectively known as *managed* registries).</span><span class="sxs-lookup"><span data-stu-id="5efed-105">The initial release of ACR offered a single SKU, Classic, that lacks several features inherent to the Basic, Standard, and Premium SKUs (collectively known as *managed* registries).</span></span>

<span data-ttu-id="5efed-106">The Classic SKU is being deprecated, and will be unavailable after March 2019.</span><span class="sxs-lookup"><span data-stu-id="5efed-106">The Classic SKU is being deprecated, and will be unavailable after March 2019.</span></span> <span data-ttu-id="5efed-107">This article details how to migrate your unmanaged Classic registry to one of the managed SKUs so that you can take advantage of their enhanced feature set.</span><span class="sxs-lookup"><span data-stu-id="5efed-107">This article details how to migrate your unmanaged Classic registry to one of the managed SKUs so that you can take advantage of their enhanced feature set.</span></span>

## <a name="why-upgrade"></a><span data-ttu-id="5efed-108">Why upgrade?</span><span class="sxs-lookup"><span data-stu-id="5efed-108">Why upgrade?</span></span>

<span data-ttu-id="5efed-109">The Classic registry SKU is being **deprecated**, and will be unavailable from **March 2019**.</span><span class="sxs-lookup"><span data-stu-id="5efed-109">The Classic registry SKU is being **deprecated**, and will be unavailable from **March 2019**.</span></span> <span data-ttu-id="5efed-110">All existing Classic registries should be upgraded prior to March 2019.</span><span class="sxs-lookup"><span data-stu-id="5efed-110">All existing Classic registries should be upgraded prior to March 2019.</span></span>

<span data-ttu-id="5efed-111">Because of the planned deprecation and limited capabilities of Classic unmanaged registries, all Classic registries be upgraded to Basic, Standard, or Premium managed registries.</span><span class="sxs-lookup"><span data-stu-id="5efed-111">Because of the planned deprecation and limited capabilities of Classic unmanaged registries, all Classic registries be upgraded to Basic, Standard, or Premium managed registries.</span></span> <span data-ttu-id="5efed-112">These higher-level SKUs more deeply integrate the registry into the capabilities of Azure.</span><span class="sxs-lookup"><span data-stu-id="5efed-112">These higher-level SKUs more deeply integrate the registry into the capabilities of Azure.</span></span>

<span data-ttu-id="5efed-113">Managed registries provide:</span><span class="sxs-lookup"><span data-stu-id="5efed-113">Managed registries provide:</span></span>

* <span data-ttu-id="5efed-114">Azure Active Directory integration for [individual login](container-registry-authentication.md#individual-login-with-azure-ad)</span><span class="sxs-lookup"><span data-stu-id="5efed-114">Azure Active Directory integration for [individual login](container-registry-authentication.md#individual-login-with-azure-ad)</span></span>
* <span data-ttu-id="5efed-115">Image and tag deletion support</span><span class="sxs-lookup"><span data-stu-id="5efed-115">Image and tag deletion support</span></span>
* [<span data-ttu-id="5efed-116">Geo-replication</span><span class="sxs-lookup"><span data-stu-id="5efed-116">Geo-replication</span></span>](container-registry-geo-replication.md)
* [<span data-ttu-id="5efed-117">Webhooks</span><span class="sxs-lookup"><span data-stu-id="5efed-117">Webhooks</span></span>](container-registry-webhook.md)

<span data-ttu-id="5efed-118">The Classic registry depends on the storage account that Azure automatically provisions in your Azure subscription when you create the registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-118">The Classic registry depends on the storage account that Azure automatically provisions in your Azure subscription when you create the registry.</span></span> <span data-ttu-id="5efed-119">By contrast, the Basic, Standard, and Premium SKUs take advantage of Azure's [advanced storage features](container-registry-storage.md) by transparently handling the storage of your images for you.</span><span class="sxs-lookup"><span data-stu-id="5efed-119">By contrast, the Basic, Standard, and Premium SKUs take advantage of Azure's [advanced storage features](container-registry-storage.md) by transparently handling the storage of your images for you.</span></span> <span data-ttu-id="5efed-120">A separate storage account is not created in your own subscription.</span><span class="sxs-lookup"><span data-stu-id="5efed-120">A separate storage account is not created in your own subscription.</span></span>

<span data-ttu-id="5efed-121">Managed registry storage provides the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5efed-121">Managed registry storage provides the following benefits:</span></span>

* <span data-ttu-id="5efed-122">Container images are [encrypted at rest](container-registry-storage.md#encryption-at-rest).</span><span class="sxs-lookup"><span data-stu-id="5efed-122">Container images are [encrypted at rest](container-registry-storage.md#encryption-at-rest).</span></span>
* <span data-ttu-id="5efed-123">Images are stored using [geo-redundant storage](container-registry-storage.md#geo-redundant-storage), assuring backup of your images with multi-region replication.</span><span class="sxs-lookup"><span data-stu-id="5efed-123">Images are stored using [geo-redundant storage](container-registry-storage.md#geo-redundant-storage), assuring backup of your images with multi-region replication.</span></span>
* <span data-ttu-id="5efed-124">Ability to freely [move between SKUs](container-registry-skus.md#changing-skus), enabling higher throughput when you choose a higher-level SKU.</span><span class="sxs-lookup"><span data-stu-id="5efed-124">Ability to freely [move between SKUs](container-registry-skus.md#changing-skus), enabling higher throughput when you choose a higher-level SKU.</span></span> <span data-ttu-id="5efed-125">With each SKU, ACR can meet your throughput requirements as your needs increase.</span><span class="sxs-lookup"><span data-stu-id="5efed-125">With each SKU, ACR can meet your throughput requirements as your needs increase.</span></span>
* <span data-ttu-id="5efed-126">Unified security model for the registry and its storage provides simplified rights management.</span><span class="sxs-lookup"><span data-stu-id="5efed-126">Unified security model for the registry and its storage provides simplified rights management.</span></span> <span data-ttu-id="5efed-127">You manage permissions only for the container registry, without having to also manage permissions for a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="5efed-127">You manage permissions only for the container registry, without having to also manage permissions for a separate storage account.</span></span>

<span data-ttu-id="5efed-128">For additional details on image storage in ACR, see [Container image storage in Azure Container Registry](container-registry-storage.md).</span><span class="sxs-lookup"><span data-stu-id="5efed-128">For additional details on image storage in ACR, see [Container image storage in Azure Container Registry](container-registry-storage.md).</span></span>

## <a name="migration-considerations"></a><span data-ttu-id="5efed-129">Migration considerations</span><span class="sxs-lookup"><span data-stu-id="5efed-129">Migration considerations</span></span>

<span data-ttu-id="5efed-130">When you change a Classic registry to a managed registry, Azure must copy all existing container images from the ACR-created storage account in your subscription to a storage account managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="5efed-130">When you change a Classic registry to a managed registry, Azure must copy all existing container images from the ACR-created storage account in your subscription to a storage account managed by Azure.</span></span> <span data-ttu-id="5efed-131">Depending on the size of your registry, this process can take a few minutes to several hours.</span><span class="sxs-lookup"><span data-stu-id="5efed-131">Depending on the size of your registry, this process can take a few minutes to several hours.</span></span>

<span data-ttu-id="5efed-132">During the conversion process, all `docker push` operations are blocked, while `docker pull` continues to function.</span><span class="sxs-lookup"><span data-stu-id="5efed-132">During the conversion process, all `docker push` operations are blocked, while `docker pull` continues to function.</span></span>

<span data-ttu-id="5efed-133">Do not delete or modify the contents of the storage account backing your Classic registry during the conversion process.</span><span class="sxs-lookup"><span data-stu-id="5efed-133">Do not delete or modify the contents of the storage account backing your Classic registry during the conversion process.</span></span> <span data-ttu-id="5efed-134">Doing so can result in the corruption of your container images.</span><span class="sxs-lookup"><span data-stu-id="5efed-134">Doing so can result in the corruption of your container images.</span></span>

<span data-ttu-id="5efed-135">Once the migration is complete, the storage account in your subscription that originally backed your Classic registry is longer used by ACR.</span><span class="sxs-lookup"><span data-stu-id="5efed-135">Once the migration is complete, the storage account in your subscription that originally backed your Classic registry is longer used by ACR.</span></span> <span data-ttu-id="5efed-136">After you've verified that the migration was successful, consider deleting the storage account to help minimize cost.</span><span class="sxs-lookup"><span data-stu-id="5efed-136">After you've verified that the migration was successful, consider deleting the storage account to help minimize cost.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="5efed-137">Upgrading from Classic to one of the managed SKUs is a **one-way process**.</span><span class="sxs-lookup"><span data-stu-id="5efed-137">Upgrading from Classic to one of the managed SKUs is a **one-way process**.</span></span> <span data-ttu-id="5efed-138">Once you've converted a Classic registry to Basic, Standard, or Premium, you cannot revert to Classic.</span><span class="sxs-lookup"><span data-stu-id="5efed-138">Once you've converted a Classic registry to Basic, Standard, or Premium, you cannot revert to Classic.</span></span> <span data-ttu-id="5efed-139">You can, however, freely move between managed SKUs with sufficient capacity for your registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-139">You can, however, freely move between managed SKUs with sufficient capacity for your registry.</span></span>

## <a name="how-to-upgrade"></a><span data-ttu-id="5efed-140">How to upgrade</span><span class="sxs-lookup"><span data-stu-id="5efed-140">How to upgrade</span></span>

<span data-ttu-id="5efed-141">You can upgrade an unmanaged Classic registry to one of the managed SKUs in several ways.</span><span class="sxs-lookup"><span data-stu-id="5efed-141">You can upgrade an unmanaged Classic registry to one of the managed SKUs in several ways.</span></span> <span data-ttu-id="5efed-142">In the following sections, we describe the process for using the [Azure CLI][azure-cli] and the [Azure portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="5efed-142">In the following sections, we describe the process for using the [Azure CLI][azure-cli] and the [Azure portal][azure-portal].</span></span>

## <a name="upgrade-in-azure-cli"></a><span data-ttu-id="5efed-143">Upgrade in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5efed-143">Upgrade in Azure CLI</span></span>

<span data-ttu-id="5efed-144">To upgrade a Classic registry in the Azure CLI, execute the [az acr update][az-acr-update] command and specify the new SKU for the registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-144">To upgrade a Classic registry in the Azure CLI, execute the [az acr update][az-acr-update] command and specify the new SKU for the registry.</span></span> <span data-ttu-id="5efed-145">In the following example, a Classic registry named *myclassicregistry* is upgraded to the Premium SKU:</span><span class="sxs-lookup"><span data-stu-id="5efed-145">In the following example, a Classic registry named *myclassicregistry* is upgraded to the Premium SKU:</span></span>

```azurecli-interactive
az acr update --name myclassicregistry --sku Premium
```

<span data-ttu-id="5efed-146">When the migration is complete, you should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="5efed-146">When the migration is complete, you should see output similar to the following.</span></span> <span data-ttu-id="5efed-147">Notice that the `sku` is "Premium" and the `storageAccount` is "null," indicating that Azure now manages the image storage for this registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-147">Notice that the `sku` is "Premium" and the `storageAccount` is "null," indicating that Azure now manages the image storage for this registry.</span></span>

```JSON
{
  "adminUserEnabled": false,
  "creationDate": "2017-12-12T21:23:29.300547+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry",
  "location": "eastus",
  "loginServer": "myregistry.azurecr.io",
  "name": "myregistry",
  "provisioningState": "Succeeded",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "name": "Premium",
    "tier": "Premium"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="5efed-148">If you specify a managed registry SKU whose maximum capacity is less than the size of your Classic registry, you'll receive an error message similar to the following.</span><span class="sxs-lookup"><span data-stu-id="5efed-148">If you specify a managed registry SKU whose maximum capacity is less than the size of your Classic registry, you'll receive an error message similar to the following.</span></span>

`Cannot update the registry SKU due to reason: Registry size 12936251113 bytes exceeds the quota value 10737418240 bytes for SKU Basic. The suggested SKU is Standard.`

<span data-ttu-id="5efed-149">If you receive a similar error, run the [az acr update][az-acr-update] command again and specify the suggested SKU, which is the next-highest level SKU that can accommodate your images.</span><span class="sxs-lookup"><span data-stu-id="5efed-149">If you receive a similar error, run the [az acr update][az-acr-update] command again and specify the suggested SKU, which is the next-highest level SKU that can accommodate your images.</span></span>

## <a name="upgrade-in-azure-portal"></a><span data-ttu-id="5efed-150">Upgrade in Azure portal</span><span class="sxs-lookup"><span data-stu-id="5efed-150">Upgrade in Azure portal</span></span>

<span data-ttu-id="5efed-151">When you upgrade a Classic registry by using the Azure portal, Azure automatically selects the lowest-level SKU that can accommodate your images.</span><span class="sxs-lookup"><span data-stu-id="5efed-151">When you upgrade a Classic registry by using the Azure portal, Azure automatically selects the lowest-level SKU that can accommodate your images.</span></span> <span data-ttu-id="5efed-152">For example, if your registry contains 12 GiB in images, Azure automatically selects and converts the Classic registry to Standard (100 GiB maximum).</span><span class="sxs-lookup"><span data-stu-id="5efed-152">For example, if your registry contains 12 GiB in images, Azure automatically selects and converts the Classic registry to Standard (100 GiB maximum).</span></span>

<span data-ttu-id="5efed-153">To upgrade your Classic registry by using the Azure portal, navigate to the container registry **Overview** and select **Upgrade to managed registry**.</span><span class="sxs-lookup"><span data-stu-id="5efed-153">To upgrade your Classic registry by using the Azure portal, navigate to the container registry **Overview** and select **Upgrade to managed registry**.</span></span>

![Classic registry upgrade button in the Azure portal UI][update-classic-01-upgrade]

<span data-ttu-id="5efed-155">Select **OK** to confirm that you want to upgrade to a managed registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-155">Select **OK** to confirm that you want to upgrade to a managed registry.</span></span>

![Classic registry upgrade confirmation in the Azure portal UI][update-classic-02-confirm]

<span data-ttu-id="5efed-157">During migration, the portal indicates that the registry's **Provisioning state** is *Updating*.</span><span class="sxs-lookup"><span data-stu-id="5efed-157">During migration, the portal indicates that the registry's **Provisioning state** is *Updating*.</span></span> <span data-ttu-id="5efed-158">As mentioned earlier, `docker push` operations are disabled during the migration, and you must not delete or update the storage account used by the Classic registry while the migration is in progress--doing so can result in image corruption.</span><span class="sxs-lookup"><span data-stu-id="5efed-158">As mentioned earlier, `docker push` operations are disabled during the migration, and you must not delete or update the storage account used by the Classic registry while the migration is in progress--doing so can result in image corruption.</span></span>

![Classic registry upgrade progress in the Azure portal UI][update-classic-03-updating]

<span data-ttu-id="5efed-160">When the migration is complete, the **Provisioning state** indicates *Succeeded*, and you can once again `docker push` to your registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-160">When the migration is complete, the **Provisioning state** indicates *Succeeded*, and you can once again `docker push` to your registry.</span></span>

![Classic registry upgrade completion state in the Azure portal UI][update-classic-04-updated]

## <a name="next-steps"></a><span data-ttu-id="5efed-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="5efed-162">Next steps</span></span>

<span data-ttu-id="5efed-163">Once you've upgraded a Classic registry to Basic, Standard, or Premium, Azure no longer uses the storage account that originally backed the Classic registry.</span><span class="sxs-lookup"><span data-stu-id="5efed-163">Once you've upgraded a Classic registry to Basic, Standard, or Premium, Azure no longer uses the storage account that originally backed the Classic registry.</span></span> <span data-ttu-id="5efed-164">To reduce cost, consider deleting the storage account or the Blob container within the account that contains your old container images.</span><span class="sxs-lookup"><span data-stu-id="5efed-164">To reduce cost, consider deleting the storage account or the Blob container within the account that contains your old container images.</span></span>

<!-- IMAGES -->
[update-classic-01-upgrade]: ./media/container-registry-upgrade\update-classic-01-upgrade.png
[update-classic-02-confirm]: ./media/container-registry-upgrade\update-classic-02-confirm.png
[update-classic-03-updating]: ./media/container-registry-upgrade\update-classic-03-updating.png
[update-classic-04-updated]: ./media/container-registry-upgrade\update-classic-04-updated.png

<!-- LINKS - internal -->
[az-acr-update]: /cli/azure/acr#az-acr-update
[azure-cli]: /cli/azure/install-azure-cli
[azure-portal]: https://portal.azure.com