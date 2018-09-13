---
title: Mount an emptyDir volume in Azure Container Instances
description: Learn how to mount an emptyDir volume to share data between the containers in a container group in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 02/08/2018
ms.author: marsma
ms.openlocfilehash: 89289a7a0bb5c486c662d528c5014bdbd8eebaca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857078"
---
# <a name="mount-an-emptydir-volume-in-azure-container-instances"></a><span data-ttu-id="b86b3-103">Mount an emptyDir volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b86b3-103">Mount an emptyDir volume in Azure Container Instances</span></span>

<span data-ttu-id="b86b3-104">Learn how to mount an *emptyDir* volume to share data between the containers in a container group in Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="b86b3-104">Learn how to mount an *emptyDir* volume to share data between the containers in a container group in Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="b86b3-105">Mounting an *emptyDir* volume is currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="b86b3-105">Mounting an *emptyDir* volume is currently restricted to Linux containers.</span></span> <span data-ttu-id="b86b3-106">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="b86b3-106">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="emptydir-volume"></a><span data-ttu-id="b86b3-107">emptyDir volume</span><span class="sxs-lookup"><span data-stu-id="b86b3-107">emptyDir volume</span></span>

<span data-ttu-id="b86b3-108">The *emptyDir* volume provides a writable directory accessible to each container in a container group.</span><span class="sxs-lookup"><span data-stu-id="b86b3-108">The *emptyDir* volume provides a writable directory accessible to each container in a container group.</span></span> <span data-ttu-id="b86b3-109">Containers in the group can read and write the same files in the volume, and it can be mounted using the same or different paths in each container.</span><span class="sxs-lookup"><span data-stu-id="b86b3-109">Containers in the group can read and write the same files in the volume, and it can be mounted using the same or different paths in each container.</span></span>

<span data-ttu-id="b86b3-110">Some example uses for an *emptyDir* volume:</span><span class="sxs-lookup"><span data-stu-id="b86b3-110">Some example uses for an *emptyDir* volume:</span></span>

* <span data-ttu-id="b86b3-111">Scratch space</span><span class="sxs-lookup"><span data-stu-id="b86b3-111">Scratch space</span></span>
* <span data-ttu-id="b86b3-112">Checkpointing during long-running tasks</span><span class="sxs-lookup"><span data-stu-id="b86b3-112">Checkpointing during long-running tasks</span></span>
* <span data-ttu-id="b86b3-113">Store data retrieved by a sidecar container and served by an application container</span><span class="sxs-lookup"><span data-stu-id="b86b3-113">Store data retrieved by a sidecar container and served by an application container</span></span>

<span data-ttu-id="b86b3-114">Data in an *emptyDir* volume is persisted through container crashes.</span><span class="sxs-lookup"><span data-stu-id="b86b3-114">Data in an *emptyDir* volume is persisted through container crashes.</span></span> <span data-ttu-id="b86b3-115">Containers that are restarted, however, are not guaranteed to persist the data in an *emptyDir* volume.</span><span class="sxs-lookup"><span data-stu-id="b86b3-115">Containers that are restarted, however, are not guaranteed to persist the data in an *emptyDir* volume.</span></span>

## <a name="mount-an-emptydir-volume"></a><span data-ttu-id="b86b3-116">Mount an emptyDir volume</span><span class="sxs-lookup"><span data-stu-id="b86b3-116">Mount an emptyDir volume</span></span>

<span data-ttu-id="b86b3-117">To mount an emptyDir volume in a container instance, you must deploy using an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).</span><span class="sxs-lookup"><span data-stu-id="b86b3-117">To mount an emptyDir volume in a container instance, you must deploy using an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).</span></span>

<span data-ttu-id="b86b3-118">First, populate the `volumes` array in the container group `properties` section of the template.</span><span class="sxs-lookup"><span data-stu-id="b86b3-118">First, populate the `volumes` array in the container group `properties` section of the template.</span></span> <span data-ttu-id="b86b3-119">Next, for each container in the container group in which you'd like to mount the *emptyDir* volume, populate the `volumeMounts` array in the `properties` section of the container definition.</span><span class="sxs-lookup"><span data-stu-id="b86b3-119">Next, for each container in the container group in which you'd like to mount the *emptyDir* volume, populate the `volumeMounts` array in the `properties` section of the container definition.</span></span>

<span data-ttu-id="b86b3-120">For example, the following Resource Manager template creates a container group consisting of two containers, each of which mounts the *emptyDir* volume:</span><span class="sxs-lookup"><span data-stu-id="b86b3-120">For example, the following Resource Manager template creates a container group consisting of two containers, each of which mounts the *emptyDir* volume:</span></span>

<span data-ttu-id="b86b3-121"><!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-emptydir.json --> [!code-json[volume-emptydir](~/azure-docs-json-samples/container-instances/aci-deploy-volume-emptydir.json)]</span><span class="sxs-lookup"><span data-stu-id="b86b3-121"><!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-emptydir.json --> [!code-json[volume-emptydir](~/azure-docs-json-samples/container-instances/aci-deploy-volume-emptydir.json)]</span></span>

<span data-ttu-id="b86b3-122">To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).</span><span class="sxs-lookup"><span data-stu-id="b86b3-122">To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b86b3-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="b86b3-123">Next steps</span></span>

<span data-ttu-id="b86b3-124">Learn how to mount other volume types in Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="b86b3-124">Learn how to mount other volume types in Azure Container Instances:</span></span>

* [<span data-ttu-id="b86b3-125">Mount an Azure file share in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b86b3-125">Mount an Azure file share in Azure Container Instances</span></span>](container-instances-volume-azure-files.md)
* [<span data-ttu-id="b86b3-126">Mount a gitRepo volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b86b3-126">Mount a gitRepo volume in Azure Container Instances</span></span>](container-instances-volume-gitrepo.md)
* [<span data-ttu-id="b86b3-127">Mount a secret volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b86b3-127">Mount a secret volume in Azure Container Instances</span></span>](container-instances-volume-secret.md)