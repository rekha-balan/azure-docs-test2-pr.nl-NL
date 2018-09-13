---
title: Troubleshooting with event tracing | Microsoft Docs
description: The most common issues encountered while deploying services on Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: ''
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: 15f7abc747aa682bee5c7b15b8c7cd63322ee567
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562857"
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a><span data-ttu-id="7ce16-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ce16-103">Troubleshoot common issues when you deploy services on Azure Service Fabric</span></span>
<span data-ttu-id="7ce16-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="7ce16-104">When you're running services on your developer computer, it is easy to use [Visual Studio's debugging tools](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span> <span data-ttu-id="7ce16-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span><span class="sxs-lookup"><span data-stu-id="7ce16-105">For remote clusters, [health reports](service-fabric-view-entities-aggregated-health.md) are always a good place to start.</span></span> <span data-ttu-id="7ce16-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="7ce16-106">The easiest ways to access these reports are through PowerShell or [SFX](service-fabric-visualizing-your-cluster.md).</span></span> <span data-ttu-id="7ce16-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span><span class="sxs-lookup"><span data-stu-id="7ce16-107">This article assumes that you are debugging a remote cluster and have a basic understanding of how to use either of these tools.</span></span>

## <a name="application-crash"></a><span data-ttu-id="7ce16-108">Application crash</span><span class="sxs-lookup"><span data-stu-id="7ce16-108">Application crash</span></span>
<span data-ttu-id="7ce16-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span><span class="sxs-lookup"><span data-stu-id="7ce16-109">The "Partition is below target replica or instance count" report is a good indication that your service is crashing.</span></span> <span data-ttu-id="7ce16-110">To find out where your service is crashing takes a little more investigation.</span><span class="sxs-lookup"><span data-stu-id="7ce16-110">To find out where your service is crashing takes a little more investigation.</span></span> <span data-ttu-id="7ce16-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span><span class="sxs-lookup"><span data-stu-id="7ce16-111">When your service is running at scale, your best friend will be a set of well-thought-out traces.</span></span>  <span data-ttu-id="7ce16-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span><span class="sxs-lookup"><span data-stu-id="7ce16-112">We suggest that you try [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) for collecting those traces and using a solution such as [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) for viewing and searching the traces.</span></span>

![SFX Partition Health](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a><span data-ttu-id="7ce16-114">During service or actor initialization</span><span class="sxs-lookup"><span data-stu-id="7ce16-114">During service or actor initialization</span></span>
<span data-ttu-id="7ce16-115">Any exceptions before the service type is initialized will cause the process to crash.</span><span class="sxs-lookup"><span data-stu-id="7ce16-115">Any exceptions before the service type is initialized will cause the process to crash.</span></span> <span data-ttu-id="7ce16-116">For these types of crashes, the application event log will show the error from your service.</span><span class="sxs-lookup"><span data-stu-id="7ce16-116">For these types of crashes, the application event log will show the error from your service.</span></span>
<span data-ttu-id="7ce16-117">These are the most common exceptions to see before the service is initialized.</span><span class="sxs-lookup"><span data-stu-id="7ce16-117">These are the most common exceptions to see before the service is initialized.</span></span>

<span data-ttu-id="7ce16-118">***System.IO.FileNotFoundException***</span><span class="sxs-lookup"><span data-stu-id="7ce16-118">***System.IO.FileNotFoundException***</span></span>

<span data-ttu-id="7ce16-119">This error is often due to missing assembly dependencies.</span><span class="sxs-lookup"><span data-stu-id="7ce16-119">This error is often due to missing assembly dependencies.</span></span> <span data-ttu-id="7ce16-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span><span class="sxs-lookup"><span data-stu-id="7ce16-120">Check the CopyLocal property in Visual Studio or the global assembly cache for the node.</span></span>

<span data-ttu-id="7ce16-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span><span class="sxs-lookup"><span data-stu-id="7ce16-121">***System.Runtime.InteropServices.COMException*** *at System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory(IntPtr, IFabricStatefulServiceFactory)*</span></span>

 <span data-ttu-id="7ce16-122">This indicates that the registered service type name does not match the service manifest.</span><span class="sxs-lookup"><span data-stu-id="7ce16-122">This indicates that the registered service type name does not match the service manifest.</span></span>

<span data-ttu-id="7ce16-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span><span class="sxs-lookup"><span data-stu-id="7ce16-123">[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) can be configured to upload the application event log for all your nodes automatically.</span></span>

### <a name="runasync-or-onactivateasync"></a><span data-ttu-id="7ce16-124">RunAsync() or OnActivateAsync()</span><span class="sxs-lookup"><span data-stu-id="7ce16-124">RunAsync() or OnActivateAsync()</span></span>
<span data-ttu-id="7ce16-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ce16-125">If the crash happens during the initialization or running of your registered service type or actor, the exception will be caught by Azure Service Fabric.</span></span> <span data-ttu-id="7ce16-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span><span class="sxs-lookup"><span data-stu-id="7ce16-126">You can view these from the EventSource providers detailed in the "Next steps" section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ce16-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ce16-127">Next steps</span></span>
<span data-ttu-id="7ce16-128">Learn more about existing diagnostics provided by Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="7ce16-128">Learn more about existing diagnostics provided by Service Fabric:</span></span>

* [<span data-ttu-id="7ce16-129">Reliable Actors diagnostics</span><span class="sxs-lookup"><span data-stu-id="7ce16-129">Reliable Actors diagnostics</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="7ce16-130">Reliable Services diagnostics</span><span class="sxs-lookup"><span data-stu-id="7ce16-130">Reliable Services diagnostics</span></span>](service-fabric-reliable-services-diagnostics.md)


