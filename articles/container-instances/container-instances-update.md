---
title: Update containers in Azure Container Instances
description: Learn how to update running containers in your Azure Container Instances container groups.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 08/01/2018
ms.author: marsma
ms.openlocfilehash: 5a42b0983b0f754b119fa304317e758a976fb4f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967420"
---
# <a name="update-containers-in-azure-container-instances"></a><span data-ttu-id="95167-103">Update containers in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="95167-103">Update containers in Azure Container Instances</span></span>

<span data-ttu-id="95167-104">During normal operation of your container instances, you may find it necessary to update the containers in a container group.</span><span class="sxs-lookup"><span data-stu-id="95167-104">During normal operation of your container instances, you may find it necessary to update the containers in a container group.</span></span> <span data-ttu-id="95167-105">For example, you might wish to update the image version, change a DNS name, update environment variables, or refresh the state of a container whose application has crashed.</span><span class="sxs-lookup"><span data-stu-id="95167-105">For example, you might wish to update the image version, change a DNS name, update environment variables, or refresh the state of a container whose application has crashed.</span></span>

## <a name="update-a-container-group"></a><span data-ttu-id="95167-106">Update a container group</span><span class="sxs-lookup"><span data-stu-id="95167-106">Update a container group</span></span>

<span data-ttu-id="95167-107">Update the containers in a container group by redeploying an existing group with at least one modified property.</span><span class="sxs-lookup"><span data-stu-id="95167-107">Update the containers in a container group by redeploying an existing group with at least one modified property.</span></span> <span data-ttu-id="95167-108">When you update a container group, all running containers in the group are restarted in-place.</span><span class="sxs-lookup"><span data-stu-id="95167-108">When you update a container group, all running containers in the group are restarted in-place.</span></span>

<span data-ttu-id="95167-109">Redeploy an existing container group by issuing the create command (or use the Azure portal) and specify the name of an existing group.</span><span class="sxs-lookup"><span data-stu-id="95167-109">Redeploy an existing container group by issuing the create command (or use the Azure portal) and specify the name of an existing group.</span></span> <span data-ttu-id="95167-110">Modify at least one valid property of the group when you issue the create command to trigger the redeployment.</span><span class="sxs-lookup"><span data-stu-id="95167-110">Modify at least one valid property of the group when you issue the create command to trigger the redeployment.</span></span> <span data-ttu-id="95167-111">Not all container group properties are valid for redeployment.</span><span class="sxs-lookup"><span data-stu-id="95167-111">Not all container group properties are valid for redeployment.</span></span> <span data-ttu-id="95167-112">See [Properties that require delete](#properties-that-require-delete) for a list of unsupported properties.</span><span class="sxs-lookup"><span data-stu-id="95167-112">See [Properties that require delete](#properties-that-require-delete) for a list of unsupported properties.</span></span>

<span data-ttu-id="95167-113">The following Azure CLI example updates a container group with a new DNS name label.</span><span class="sxs-lookup"><span data-stu-id="95167-113">The following Azure CLI example updates a container group with a new DNS name label.</span></span> <span data-ttu-id="95167-114">Because the DNS name label property of the group is modified, the container group is redeployed, and its containers restarted.</span><span class="sxs-lookup"><span data-stu-id="95167-114">Because the DNS name label property of the group is modified, the container group is redeployed, and its containers restarted.</span></span>

<span data-ttu-id="95167-115">Initial deployment with DNS name label *myapplication-staging*:</span><span class="sxs-lookup"><span data-stu-id="95167-115">Initial deployment with DNS name label *myapplication-staging*:</span></span>

```azurecli-interactive
# Create container group
az container create --resource-group myResourceGroup --name mycontainer \
    --image nginx:alpine --dns-name-label myapplication-staging
```

<span data-ttu-id="95167-116">Update the container group with a new DNS name label, *myapplication*:</span><span class="sxs-lookup"><span data-stu-id="95167-116">Update the container group with a new DNS name label, *myapplication*:</span></span>

```azurecli-interactive
# Update container group (restarts container)
az container create --resource-group myResourceGroup --name mycontainer \
    --image nginx:alpine --dns-name-label myapplication
```

## <a name="update-benefits"></a><span data-ttu-id="95167-117">Update benefits</span><span class="sxs-lookup"><span data-stu-id="95167-117">Update benefits</span></span>

<span data-ttu-id="95167-118">The primary benefit of updating an existing container group is faster deployment.</span><span class="sxs-lookup"><span data-stu-id="95167-118">The primary benefit of updating an existing container group is faster deployment.</span></span> <span data-ttu-id="95167-119">When you redeploy an existing container group, its container image layers are pulled from those cached by the previous deployment.</span><span class="sxs-lookup"><span data-stu-id="95167-119">When you redeploy an existing container group, its container image layers are pulled from those cached by the previous deployment.</span></span> <span data-ttu-id="95167-120">Instead of pulling all image layers fresh from the registry as is done with new deployments, only modified layers (if any) are pulled.</span><span class="sxs-lookup"><span data-stu-id="95167-120">Instead of pulling all image layers fresh from the registry as is done with new deployments, only modified layers (if any) are pulled.</span></span>

<span data-ttu-id="95167-121">Applications based on larger container images like Windows Server Core can see significant improvement in deployment speed when you update instead of delete and deploy new.</span><span class="sxs-lookup"><span data-stu-id="95167-121">Applications based on larger container images like Windows Server Core can see significant improvement in deployment speed when you update instead of delete and deploy new.</span></span>

## <a name="limitations"></a><span data-ttu-id="95167-122">Limitations</span><span class="sxs-lookup"><span data-stu-id="95167-122">Limitations</span></span>

<span data-ttu-id="95167-123">Not all properties of a container group support updates.</span><span class="sxs-lookup"><span data-stu-id="95167-123">Not all properties of a container group support updates.</span></span> <span data-ttu-id="95167-124">To change some properties of a container group, you must first delete, then redeploy the group.</span><span class="sxs-lookup"><span data-stu-id="95167-124">To change some properties of a container group, you must first delete, then redeploy the group.</span></span> <span data-ttu-id="95167-125">For details, see [Properties that require container delete](#properties-that-require-container-delete).</span><span class="sxs-lookup"><span data-stu-id="95167-125">For details, see [Properties that require container delete](#properties-that-require-container-delete).</span></span>

<span data-ttu-id="95167-126">All containers in a container group are restarted when you update the container group.</span><span class="sxs-lookup"><span data-stu-id="95167-126">All containers in a container group are restarted when you update the container group.</span></span> <span data-ttu-id="95167-127">You can't perform an update or in-place restart of a specific container in a multi-container group.</span><span class="sxs-lookup"><span data-stu-id="95167-127">You can't perform an update or in-place restart of a specific container in a multi-container group.</span></span>

<span data-ttu-id="95167-128">The IP address of a container won't typically change between updates, but it's not guaranteed to remain the same.</span><span class="sxs-lookup"><span data-stu-id="95167-128">The IP address of a container won't typically change between updates, but it's not guaranteed to remain the same.</span></span> <span data-ttu-id="95167-129">As long as the container group is deployed to the same underlying host, the container group retains its IP address.</span><span class="sxs-lookup"><span data-stu-id="95167-129">As long as the container group is deployed to the same underlying host, the container group retains its IP address.</span></span> <span data-ttu-id="95167-130">Although rare, and while Azure Container Instances makes every effort to redeploy to the same host, there are some Azure-internal events that can cause redeployment to a different host.</span><span class="sxs-lookup"><span data-stu-id="95167-130">Although rare, and while Azure Container Instances makes every effort to redeploy to the same host, there are some Azure-internal events that can cause redeployment to a different host.</span></span> <span data-ttu-id="95167-131">To mitigate this issue, always use a DNS name label for your container instances.</span><span class="sxs-lookup"><span data-stu-id="95167-131">To mitigate this issue, always use a DNS name label for your container instances.</span></span>

<span data-ttu-id="95167-132">Terminated or deleted container groups can't be updated.</span><span class="sxs-lookup"><span data-stu-id="95167-132">Terminated or deleted container groups can't be updated.</span></span> <span data-ttu-id="95167-133">Once a container group has stopped (is in the *Terminated* state) or has been deleted, the group is deployed as new.</span><span class="sxs-lookup"><span data-stu-id="95167-133">Once a container group has stopped (is in the *Terminated* state) or has been deleted, the group is deployed as new.</span></span>

## <a name="properties-that-require-container-delete"></a><span data-ttu-id="95167-134">Properties that require container delete</span><span class="sxs-lookup"><span data-stu-id="95167-134">Properties that require container delete</span></span>

<span data-ttu-id="95167-135">As mentioned earlier, not all container group properties can be updated.</span><span class="sxs-lookup"><span data-stu-id="95167-135">As mentioned earlier, not all container group properties can be updated.</span></span> <span data-ttu-id="95167-136">For example, to change the ports or restart policy of a container, you must first delete the container group, then create it again.</span><span class="sxs-lookup"><span data-stu-id="95167-136">For example, to change the ports or restart policy of a container, you must first delete the container group, then create it again.</span></span>

<span data-ttu-id="95167-137">These properties require container group deletion prior to redeployment:</span><span class="sxs-lookup"><span data-stu-id="95167-137">These properties require container group deletion prior to redeployment:</span></span>

* <span data-ttu-id="95167-138">OS type</span><span class="sxs-lookup"><span data-stu-id="95167-138">OS type</span></span>
* <span data-ttu-id="95167-139">CPU</span><span class="sxs-lookup"><span data-stu-id="95167-139">CPU</span></span>
* <span data-ttu-id="95167-140">Memory</span><span class="sxs-lookup"><span data-stu-id="95167-140">Memory</span></span>
* <span data-ttu-id="95167-141">Restart policy</span><span class="sxs-lookup"><span data-stu-id="95167-141">Restart policy</span></span>
* <span data-ttu-id="95167-142">Ports</span><span class="sxs-lookup"><span data-stu-id="95167-142">Ports</span></span>

<span data-ttu-id="95167-143">When you delete a container group and recreate it, it's not "redeployed," but created new.</span><span class="sxs-lookup"><span data-stu-id="95167-143">When you delete a container group and recreate it, it's not "redeployed," but created new.</span></span> <span data-ttu-id="95167-144">All image layers are pulled fresh from the registry, not from those cached by a previous deployment.</span><span class="sxs-lookup"><span data-stu-id="95167-144">All image layers are pulled fresh from the registry, not from those cached by a previous deployment.</span></span> <span data-ttu-id="95167-145">The IP address of the container might also change due to being deployed to a different underlying host.</span><span class="sxs-lookup"><span data-stu-id="95167-145">The IP address of the container might also change due to being deployed to a different underlying host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95167-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="95167-146">Next steps</span></span>

<span data-ttu-id="95167-147">Mentioned several times in this article is the **container group**.</span><span class="sxs-lookup"><span data-stu-id="95167-147">Mentioned several times in this article is the **container group**.</span></span> <span data-ttu-id="95167-148">Every container in Azure Container Instances is deployed in a container group, and container groups can contain more than one container.</span><span class="sxs-lookup"><span data-stu-id="95167-148">Every container in Azure Container Instances is deployed in a container group, and container groups can contain more than one container.</span></span>

[<span data-ttu-id="95167-149">Container groups in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="95167-149">Container groups in Azure Container Instances</span></span>](container-instances-container-groups.md)

[<span data-ttu-id="95167-150">Deploy a multi-container group</span><span class="sxs-lookup"><span data-stu-id="95167-150">Deploy a multi-container group</span></span>](container-instances-multi-container-group.md)

<!-- LINKS - External -->

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container?view=azure-cli-latest#az-container-create
[az-container-logs]: /cli/azure/container?view=azure-cli-latest#az-container-logs
[az-container-show]: /cli/azure/container?view=azure-cli-latest#az-container-show
[azure-cli-install]: /cli/azure/install-azure-cli
