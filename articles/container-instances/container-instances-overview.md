---
title: Azure Container Instances overview
description: Understand Azure Container Instances
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 07/19/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 953d1dfd633f2fee52a2e6d197c6f32e7ab053f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866483"
---
# <a name="azure-container-instances"></a><span data-ttu-id="407cd-103">Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="407cd-103">Azure Container Instances</span></span>

<span data-ttu-id="407cd-104">Containers are becoming the preferred way to package, deploy, and manage cloud applications.</span><span class="sxs-lookup"><span data-stu-id="407cd-104">Containers are becoming the preferred way to package, deploy, and manage cloud applications.</span></span> <span data-ttu-id="407cd-105">Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to manage any virtual machines and without having to adopt a higher-level service.</span><span class="sxs-lookup"><span data-stu-id="407cd-105">Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to manage any virtual machines and without having to adopt a higher-level service.</span></span>

<span data-ttu-id="407cd-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span><span class="sxs-lookup"><span data-stu-id="407cd-106">Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="407cd-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend [Azure Kubernetes Service (AKS)](../aks/index.yml).</span><span class="sxs-lookup"><span data-stu-id="407cd-107">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend [Azure Kubernetes Service (AKS)](../aks/index.yml).</span></span>

## <a name="fast-startup-times"></a><span data-ttu-id="407cd-108">Fast startup times</span><span class="sxs-lookup"><span data-stu-id="407cd-108">Fast startup times</span></span>

<span data-ttu-id="407cd-109">Containers offer significant startup benefits over virtual machines.</span><span class="sxs-lookup"><span data-stu-id="407cd-109">Containers offer significant startup benefits over virtual machines.</span></span> <span data-ttu-id="407cd-110">Azure Container Instances can start containers in Azure in seconds, without the need to provision and manage VMs.</span><span class="sxs-lookup"><span data-stu-id="407cd-110">Azure Container Instances can start containers in Azure in seconds, without the need to provision and manage VMs.</span></span>

## <a name="public-ip-connectivity-and-dns-name"></a><span data-ttu-id="407cd-111">Public IP connectivity and DNS name</span><span class="sxs-lookup"><span data-stu-id="407cd-111">Public IP connectivity and DNS name</span></span>

<span data-ttu-id="407cd-112">Azure Container Instances enables exposing your containers directly to the internet with an IP address and a fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="407cd-112">Azure Container Instances enables exposing your containers directly to the internet with an IP address and a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="407cd-113">When you create a container instance, you can specify a custom DNS name label so your application is reachable at *customlabel*.*azureregion*.azurecontainer.io.</span><span class="sxs-lookup"><span data-stu-id="407cd-113">When you create a container instance, you can specify a custom DNS name label so your application is reachable at *customlabel*.*azureregion*.azurecontainer.io.</span></span>

## <a name="hypervisor-level-security"></a><span data-ttu-id="407cd-114">Hypervisor-level security</span><span class="sxs-lookup"><span data-stu-id="407cd-114">Hypervisor-level security</span></span>

<span data-ttu-id="407cd-115">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span><span class="sxs-lookup"><span data-stu-id="407cd-115">Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage.</span></span> <span data-ttu-id="407cd-116">Azure Container Instances guarantees your application is as isolated in a container as it would be in a VM.</span><span class="sxs-lookup"><span data-stu-id="407cd-116">Azure Container Instances guarantees your application is as isolated in a container as it would be in a VM.</span></span>

## <a name="custom-sizes"></a><span data-ttu-id="407cd-117">Custom sizes</span><span class="sxs-lookup"><span data-stu-id="407cd-117">Custom sizes</span></span>

<span data-ttu-id="407cd-118">Containers are typically optimized to run just a single application, but the exact needs of those applications can differ greatly.</span><span class="sxs-lookup"><span data-stu-id="407cd-118">Containers are typically optimized to run just a single application, but the exact needs of those applications can differ greatly.</span></span> <span data-ttu-id="407cd-119">Azure Container Instances provides optimum utilization by allowing exact specifications of CPU cores and memory.</span><span class="sxs-lookup"><span data-stu-id="407cd-119">Azure Container Instances provides optimum utilization by allowing exact specifications of CPU cores and memory.</span></span> <span data-ttu-id="407cd-120">You pay based on what you need and get billed by the second, so you can fine-tune your spending based on actual need.</span><span class="sxs-lookup"><span data-stu-id="407cd-120">You pay based on what you need and get billed by the second, so you can fine-tune your spending based on actual need.</span></span>

## <a name="persistent-storage"></a><span data-ttu-id="407cd-121">Persistent storage</span><span class="sxs-lookup"><span data-stu-id="407cd-121">Persistent storage</span></span>

<span data-ttu-id="407cd-122">To retrieve and persist state with Azure Container Instances, we offer direct [mounting of Azure Files shares](container-instances-mounting-azure-files-volume.md).</span><span class="sxs-lookup"><span data-stu-id="407cd-122">To retrieve and persist state with Azure Container Instances, we offer direct [mounting of Azure Files shares](container-instances-mounting-azure-files-volume.md).</span></span>

## <a name="linux-and-windows-containers"></a><span data-ttu-id="407cd-123">Linux and Windows containers</span><span class="sxs-lookup"><span data-stu-id="407cd-123">Linux and Windows containers</span></span>

<span data-ttu-id="407cd-124">Azure Container Instances can schedule both Windows and Linux containers with the same API.</span><span class="sxs-lookup"><span data-stu-id="407cd-124">Azure Container Instances can schedule both Windows and Linux containers with the same API.</span></span> <span data-ttu-id="407cd-125">Simply specify the OS type when you create your [container groups](container-instances-container-groups.md).</span><span class="sxs-lookup"><span data-stu-id="407cd-125">Simply specify the OS type when you create your [container groups](container-instances-container-groups.md).</span></span>

<span data-ttu-id="407cd-126">Some features are currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="407cd-126">Some features are currently restricted to Linux containers.</span></span> <span data-ttu-id="407cd-127">While we work to bring feature parity to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="407cd-127">While we work to bring feature parity to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

<span data-ttu-id="407cd-128">Azure Container Instances supports Windows images based on Long-Term Servicing Channel (LTSC) versions.</span><span class="sxs-lookup"><span data-stu-id="407cd-128">Azure Container Instances supports Windows images based on Long-Term Servicing Channel (LTSC) versions.</span></span> <span data-ttu-id="407cd-129">Windows Semi-Annual Channel (SAC) releases like 1709 and 1803 are unsupported.</span><span class="sxs-lookup"><span data-stu-id="407cd-129">Windows Semi-Annual Channel (SAC) releases like 1709 and 1803 are unsupported.</span></span>

## <a name="co-scheduled-groups"></a><span data-ttu-id="407cd-130">Co-scheduled groups</span><span class="sxs-lookup"><span data-stu-id="407cd-130">Co-scheduled groups</span></span>

<span data-ttu-id="407cd-131">Azure Container Instances supports scheduling of [multi-container groups](container-instances-container-groups.md) that share a host machine, local network, storage, and lifecycle.</span><span class="sxs-lookup"><span data-stu-id="407cd-131">Azure Container Instances supports scheduling of [multi-container groups](container-instances-container-groups.md) that share a host machine, local network, storage, and lifecycle.</span></span> <span data-ttu-id="407cd-132">This enables you to combine your main application container with other supporting role containers, such as logging sidecars.</span><span class="sxs-lookup"><span data-stu-id="407cd-132">This enables you to combine your main application container with other supporting role containers, such as logging sidecars.</span></span>

## <a name="next-steps"></a><span data-ttu-id="407cd-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="407cd-133">Next steps</span></span>

<span data-ttu-id="407cd-134">Try deploying a container to Azure with a single command using our quickstart guide:</span><span class="sxs-lookup"><span data-stu-id="407cd-134">Try deploying a container to Azure with a single command using our quickstart guide:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="407cd-135">Azure Container Instances Quickstart</span><span class="sxs-lookup"><span data-stu-id="407cd-135">Azure Container Instances Quickstart</span></span>](container-instances-quickstart.md)
