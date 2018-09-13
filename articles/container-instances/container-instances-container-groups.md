---
title: Azure Container Instances container groups
description: Understand how container groups work in Azure Container Instances
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 03/20/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: cb3d8c27a82c7dfc5fd71c1c7d589e81890e5cfb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856145"
---
# <a name="container-groups-in-azure-container-instances"></a><span data-ttu-id="b2ebe-103">Container groups in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="b2ebe-103">Container groups in Azure Container Instances</span></span>

<span data-ttu-id="b2ebe-104">The top-level resource in Azure Container Instances is the *container group*.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-104">The top-level resource in Azure Container Instances is the *container group*.</span></span> <span data-ttu-id="b2ebe-105">This article describes what container groups are and the types of scenarios they enable.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-105">This article describes what container groups are and the types of scenarios they enable.</span></span>

## <a name="how-a-container-group-works"></a><span data-ttu-id="b2ebe-106">How a container group works</span><span class="sxs-lookup"><span data-stu-id="b2ebe-106">How a container group works</span></span>

<span data-ttu-id="b2ebe-107">A container group is a collection of containers that get scheduled on the same host machine.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-107">A container group is a collection of containers that get scheduled on the same host machine.</span></span> <span data-ttu-id="b2ebe-108">The containers in a container group share a lifecycle, local network, and storage volumes.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-108">The containers in a container group share a lifecycle, local network, and storage volumes.</span></span> <span data-ttu-id="b2ebe-109">It's similar in concept to a *pod* in [Kubernetes][kubernetes-pod] and [DC/OS][dcos-pod].</span><span class="sxs-lookup"><span data-stu-id="b2ebe-109">It's similar in concept to a *pod* in [Kubernetes][kubernetes-pod] and [DC/OS][dcos-pod].</span></span>

<span data-ttu-id="b2ebe-110">The following diagram shows an example of a container group that includes multiple containers:</span><span class="sxs-lookup"><span data-stu-id="b2ebe-110">The following diagram shows an example of a container group that includes multiple containers:</span></span>

![Container groups diagram][container-groups-example]

<span data-ttu-id="b2ebe-112">This example container group:</span><span class="sxs-lookup"><span data-stu-id="b2ebe-112">This example container group:</span></span>

* <span data-ttu-id="b2ebe-113">Is scheduled on a single host machine.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-113">Is scheduled on a single host machine.</span></span>
* <span data-ttu-id="b2ebe-114">Is assigned a DNS name label.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-114">Is assigned a DNS name label.</span></span>
* <span data-ttu-id="b2ebe-115">Exposes a single public IP address, with one exposed port.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-115">Exposes a single public IP address, with one exposed port.</span></span>
* <span data-ttu-id="b2ebe-116">Consists of two containers.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-116">Consists of two containers.</span></span> <span data-ttu-id="b2ebe-117">One container listens on port 80, while the other listens on port 5000.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-117">One container listens on port 80, while the other listens on port 5000.</span></span>
* <span data-ttu-id="b2ebe-118">Includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-118">Includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.</span></span>

> [!NOTE]
> <span data-ttu-id="b2ebe-119">Multi-container groups are currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-119">Multi-container groups are currently restricted to Linux containers.</span></span> <span data-ttu-id="b2ebe-120">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="b2ebe-120">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="deployment"></a><span data-ttu-id="b2ebe-121">Deployment</span><span class="sxs-lookup"><span data-stu-id="b2ebe-121">Deployment</span></span>

<span data-ttu-id="b2ebe-122">Container *groups* have a minimum resource allocation of 1 vCPU and 1 GB memory.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-122">Container *groups* have a minimum resource allocation of 1 vCPU and 1 GB memory.</span></span> <span data-ttu-id="b2ebe-123">Individual *containers* within a container group can be provisioned with less than 1 vCPU and 1 GB memory.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-123">Individual *containers* within a container group can be provisioned with less than 1 vCPU and 1 GB memory.</span></span> <span data-ttu-id="b2ebe-124">Within a container group, the distribution of resources can be customized to multiple containers within the limits established at the container group-level.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-124">Within a container group, the distribution of resources can be customized to multiple containers within the limits established at the container group-level.</span></span> <span data-ttu-id="b2ebe-125">For example, two containers each with 0.5 vCPU residing in a container group that's allocated 1 vCPU.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-125">For example, two containers each with 0.5 vCPU residing in a container group that's allocated 1 vCPU.</span></span>

## <a name="networking"></a><span data-ttu-id="b2ebe-126">Networking</span><span class="sxs-lookup"><span data-stu-id="b2ebe-126">Networking</span></span>

<span data-ttu-id="b2ebe-127">Container groups share an IP address and a port namespace on that IP address.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-127">Container groups share an IP address and a port namespace on that IP address.</span></span> <span data-ttu-id="b2ebe-128">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-128">To enable external clients to reach a container within the group, you must expose the port on the IP address and from the container.</span></span> <span data-ttu-id="b2ebe-129">Because containers within the group share a port namespace, port mapping is not supported.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-129">Because containers within the group share a port namespace, port mapping is not supported.</span></span> <span data-ttu-id="b2ebe-130">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-130">Containers within a group can reach each other via localhost on the ports that they have exposed, even if those ports are not exposed externally on the group's IP address.</span></span>

## <a name="storage"></a><span data-ttu-id="b2ebe-131">Storage</span><span class="sxs-lookup"><span data-stu-id="b2ebe-131">Storage</span></span>

<span data-ttu-id="b2ebe-132">You can specify external volumes to mount within a container group.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-132">You can specify external volumes to mount within a container group.</span></span> <span data-ttu-id="b2ebe-133">You can map those volumes into specific paths within the individual containers in a group.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-133">You can map those volumes into specific paths within the individual containers in a group.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="b2ebe-134">Common scenarios</span><span class="sxs-lookup"><span data-stu-id="b2ebe-134">Common scenarios</span></span>

<span data-ttu-id="b2ebe-135">Multi-container groups are useful in cases where you want to divide a single functional task into a small number of container images.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-135">Multi-container groups are useful in cases where you want to divide a single functional task into a small number of container images.</span></span> <span data-ttu-id="b2ebe-136">These images can then be delivered by different teams and have separate resource requirements.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-136">These images can then be delivered by different teams and have separate resource requirements.</span></span>

<span data-ttu-id="b2ebe-137">Example usage could include:</span><span class="sxs-lookup"><span data-stu-id="b2ebe-137">Example usage could include:</span></span>

* <span data-ttu-id="b2ebe-138">An application container and a logging container.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-138">An application container and a logging container.</span></span> <span data-ttu-id="b2ebe-139">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-139">The logging container collects the logs and metrics output by the main application and writes them to long-term storage.</span></span>
* <span data-ttu-id="b2ebe-140">An application container and a monitoring container.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-140">An application container and a monitoring container.</span></span> <span data-ttu-id="b2ebe-141">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly, and raises an alert if it's not.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-141">The monitoring container periodically makes a request to the application to ensure that it's running and responding correctly, and raises an alert if it's not.</span></span>
* <span data-ttu-id="b2ebe-142">A container serving a web application and a container pulling the latest content from source control.</span><span class="sxs-lookup"><span data-stu-id="b2ebe-142">A container serving a web application and a container pulling the latest content from source control.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2ebe-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="b2ebe-143">Next steps</span></span>

<span data-ttu-id="b2ebe-144">Learn how to deploy a multi-container container group with an Azure Resource Manager template:</span><span class="sxs-lookup"><span data-stu-id="b2ebe-144">Learn how to deploy a multi-container container group with an Azure Resource Manager template:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b2ebe-145">Deploy a container group</span><span class="sxs-lookup"><span data-stu-id="b2ebe-145">Deploy a container group</span></span>](container-instances-multi-container-group.md)

<!-- IMAGES -->
[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png

<!-- LINKS - External -->
[dcos-pod]: https://dcos.io/docs/1.10/deploying-services/pods/
[kubernetes-pod]: https://kubernetes.io/docs/concepts/workloads/pods/pod/
