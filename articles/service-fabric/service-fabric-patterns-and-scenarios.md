---
title: Azure Service Fabric patterns and scenarios | Microsoft Docs
description: Learn best practices and proven, re-usable patterns to design, develop, and operate your microservices on Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: ''
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: ryanwi
ms.openlocfilehash: da30a704e41f37e59af417ad923b7bf627e108f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550444"
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="64c77-103">Service Fabric patterns and scenarios</span><span class="sxs-lookup"><span data-stu-id="64c77-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="64c77-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span><span class="sxs-lookup"><span data-stu-id="64c77-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="64c77-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span><span class="sxs-lookup"><span data-stu-id="64c77-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="64c77-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span><span class="sxs-lookup"><span data-stu-id="64c77-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="64c77-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span><span class="sxs-lookup"><span data-stu-id="64c77-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="64c77-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span><span class="sxs-lookup"><span data-stu-id="64c77-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="64c77-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span><span class="sxs-lookup"><span data-stu-id="64c77-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="64c77-110">Introduction</span><span class="sxs-lookup"><span data-stu-id="64c77-110">Introduction</span></span>
<span data-ttu-id="64c77-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span><span class="sxs-lookup"><span data-stu-id="64c77-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="64c77-112">Get the details on following proven application design principles.</span><span class="sxs-lookup"><span data-stu-id="64c77-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="64c77-113">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-113">Video</span></span></th><th><span data-ttu-id="64c77-114">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span><span class="sxs-lookup"><span data-stu-id="64c77-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="64c77-116">Cluster planning and management</span><span class="sxs-lookup"><span data-stu-id="64c77-116">Cluster planning and management</span></span>
<span data-ttu-id="64c77-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="64c77-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="64c77-118">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-118">Video</span></span></th><th><span data-ttu-id="64c77-119">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="64c77-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span><span class="sxs-lookup"><span data-stu-id="64c77-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="64c77-121">Hyper-scale web</span><span class="sxs-lookup"><span data-stu-id="64c77-121">Hyper-scale web</span></span>
<span data-ttu-id="64c77-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span><span class="sxs-lookup"><span data-stu-id="64c77-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="64c77-123">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-123">Video</span></span></th><th><span data-ttu-id="64c77-124">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span><span class="sxs-lookup"><span data-stu-id="64c77-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="64c77-126">IoT</span><span class="sxs-lookup"><span data-stu-id="64c77-126">IoT</span></span>
<span data-ttu-id="64c77-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span><span class="sxs-lookup"><span data-stu-id="64c77-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="64c77-128">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-128">Video</span></span></th><th><span data-ttu-id="64c77-129">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="64c77-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="64c77-131">Gaming</span><span class="sxs-lookup"><span data-stu-id="64c77-131">Gaming</span></span>
<span data-ttu-id="64c77-132">Look at turn-based games, interactive games, and hosting existing game engines.</span><span class="sxs-lookup"><span data-stu-id="64c77-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="64c77-133">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-133">Video</span></span></th><th><span data-ttu-id="64c77-134">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span><span class="sxs-lookup"><span data-stu-id="64c77-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="64c77-136">Continuous delivery</span><span class="sxs-lookup"><span data-stu-id="64c77-136">Continuous delivery</span></span>
<span data-ttu-id="64c77-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span><span class="sxs-lookup"><span data-stu-id="64c77-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="64c77-138">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-138">Video</span></span></th><th><span data-ttu-id="64c77-139">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span><span class="sxs-lookup"><span data-stu-id="64c77-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="64c77-141">Migration</span><span class="sxs-lookup"><span data-stu-id="64c77-141">Migration</span></span>
<span data-ttu-id="64c77-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span><span class="sxs-lookup"><span data-stu-id="64c77-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="64c77-143">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-143">Video</span></span></th><th><span data-ttu-id="64c77-144">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span><span class="sxs-lookup"><span data-stu-id="64c77-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="64c77-146">Containers and Linux support</span><span class="sxs-lookup"><span data-stu-id="64c77-146">Containers and Linux support</span></span>
<span data-ttu-id="64c77-147">Get the answer to the question, "Why containers?"</span><span class="sxs-lookup"><span data-stu-id="64c77-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="64c77-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span><span class="sxs-lookup"><span data-stu-id="64c77-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="64c77-149">Plus, find out how to migrate .NET Core apps to Linux.</span><span class="sxs-lookup"><span data-stu-id="64c77-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="64c77-150">Video</span><span class="sxs-lookup"><span data-stu-id="64c77-150">Video</span></span></th><th><span data-ttu-id="64c77-151">PowerPoint deck</span><span class="sxs-lookup"><span data-stu-id="64c77-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="64c77-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span><span class="sxs-lookup"><span data-stu-id="64c77-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="64c77-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="64c77-153">Next steps</span></span>
<span data-ttu-id="64c77-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64c77-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>








