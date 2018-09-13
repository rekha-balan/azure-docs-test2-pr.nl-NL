---
title: Azure Container Instances and container orchestration
description: Understand how Azure container instances interact with container orchestrators.
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 03/23/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: e1455cba004facfa03dca21544eec754f5dc60be
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855669"
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="c3f4e-103">Azure Container Instances and container orchestrators</span><span class="sxs-lookup"><span data-stu-id="c3f4e-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="c3f4e-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="c3f4e-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="c3f4e-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm.</span></span>

<span data-ttu-id="c3f4e-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms.</span></span> <span data-ttu-id="c3f4e-108">And while it does not cover the higher-value services that those platforms provide, Azure Container Instances can be complementary to them.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-108">And while it does not cover the higher-value services that those platforms provide, Azure Container Instances can be complementary to them.</span></span> <span data-ttu-id="c3f4e-109">This article describes the scope of what Azure Container Instances handles, and how full container orchestrators might interact with it.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-109">This article describes the scope of what Azure Container Instances handles, and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="c3f4e-110">Traditional orchestration</span><span class="sxs-lookup"><span data-stu-id="c3f4e-110">Traditional orchestration</span></span>

<span data-ttu-id="c3f4e-111">The standard definition of orchestration includes the following tasks:</span><span class="sxs-lookup"><span data-stu-id="c3f4e-111">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="c3f4e-112">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-112">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="c3f4e-113">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span><span class="sxs-lookup"><span data-stu-id="c3f4e-113">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="c3f4e-114">**Health monitoring**: Watch for container failures and automatically reschedule them.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-114">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="c3f4e-115">**Failover**: Keep track of what is running on each machine, and reschedule containers from failed machines to healthy nodes.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-115">**Failover**: Keep track of what is running on each machine, and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="c3f4e-116">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-116">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="c3f4e-117">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-117">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="c3f4e-118">**Service discovery**: Enable containers to locate each other automatically, even as they move between host machines and change IP addresses.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-118">**Service discovery**: Enable containers to locate each other automatically, even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="c3f4e-119">**Coordinated application upgrades**: Manage container upgrades to avoid application downtime, and enable rollback if something goes wrong.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-119">**Coordinated application upgrades**: Manage container upgrades to avoid application downtime, and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="c3f4e-120">Orchestration with Azure Container Instances: A layered approach</span><span class="sxs-lookup"><span data-stu-id="c3f4e-120">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="c3f4e-121">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-121">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="c3f4e-122">Because the underlying infrastructure for container instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-122">Because the underlying infrastructure for container instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="c3f4e-123">The elasticity of the cloud ensures that one is always available.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-123">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="c3f4e-124">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-124">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>

## <a name="potential-scenarios"></a><span data-ttu-id="c3f4e-125">Potential scenarios</span><span class="sxs-lookup"><span data-stu-id="c3f4e-125">Potential scenarios</span></span>

<span data-ttu-id="c3f4e-126">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span><span class="sxs-lookup"><span data-stu-id="c3f4e-126">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="c3f4e-127">Orchestration of container instances exclusively</span><span class="sxs-lookup"><span data-stu-id="c3f4e-127">Orchestration of container instances exclusively</span></span>

<span data-ttu-id="c3f4e-128">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-128">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="c3f4e-129">Combination of container instances and containers in Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c3f4e-129">Combination of container instances and containers in Virtual Machines</span></span>

<span data-ttu-id="c3f4e-130">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines is typically cheaper than running the same containers with Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-130">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines is typically cheaper than running the same containers with Azure Container Instances.</span></span> <span data-ttu-id="c3f4e-131">However, container instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-131">However, container instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span>

<span data-ttu-id="c3f4e-132">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers in Azure Container Instances, and delete them when they're no longer needed.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-132">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers in Azure Container Instances, and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="c3f4e-133">Sample implementation: Azure Container Instances Connector for Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c3f4e-133">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="c3f4e-134">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="c3f4e-134">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span>

<span data-ttu-id="c3f4e-135">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-135">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span>

<span data-ttu-id="c3f4e-136">Connectors for other orchestrators could be built that similarly integrate with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-136">Connectors for other orchestrators could be built that similarly integrate with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="c3f4e-137">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span><span class="sxs-lookup"><span data-stu-id="c3f4e-137">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3f4e-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3f4e-138">Next steps</span></span>

<span data-ttu-id="c3f4e-139">Create your first container with Azure Container Instances using the [quickstart guide](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="c3f4e-139">Create your first container with Azure Container Instances using the [quickstart guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/virtual-kubelet/virtual-kubelet/tree/master/providers/azure
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/