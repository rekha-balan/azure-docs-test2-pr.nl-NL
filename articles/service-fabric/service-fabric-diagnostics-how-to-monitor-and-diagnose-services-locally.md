---
title: Debug Azure microservices in Windows | Microsoft Docs
description: Learn how to monitor and diagnose your services written using Microsoft Azure Service Fabric on a local development machine.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: ''
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: dekapur
ms.openlocfilehash: 1405f4a9f267ec700f3b0b6c5083c89dbf03b78d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556385"
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="8375e-103">Monitor and diagnose services in a local machine development setup</span><span class="sxs-lookup"><span data-stu-id="8375e-103">Monitor and diagnose services in a local machine development setup</span></span>
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
> 
> 

<span data-ttu-id="8375e-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span><span class="sxs-lookup"><span data-stu-id="8375e-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="8375e-107">While monitoring and diagnostics are critical in an actual deployed production environment, the efficiency will depend on adopting a similar model during development of services to ensure they work when you move to a real-world setup.</span><span class="sxs-lookup"><span data-stu-id="8375e-107">While monitoring and diagnostics are critical in an actual deployed production environment, the efficiency will depend on adopting a similar model during development of services to ensure they work when you move to a real-world setup.</span></span> <span data-ttu-id="8375e-108">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span><span class="sxs-lookup"><span data-stu-id="8375e-108">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>

## <a name="the-benefits-of-event-tracing-for-windows"></a><span data-ttu-id="8375e-109">The benefits of Event Tracing for Windows</span><span class="sxs-lookup"><span data-stu-id="8375e-109">The benefits of Event Tracing for Windows</span></span>
<span data-ttu-id="8375e-110">[Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) is the recommended technology for tracing messages in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8375e-110">[Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) is the recommended technology for tracing messages in Service Fabric.</span></span> <span data-ttu-id="8375e-111">Reasons for this are:</span><span class="sxs-lookup"><span data-stu-id="8375e-111">Reasons for this are:</span></span>

* <span data-ttu-id="8375e-112">**ETW is fast.**</span><span class="sxs-lookup"><span data-stu-id="8375e-112">**ETW is fast.**</span></span> <span data-ttu-id="8375e-113">It was built as a tracing technology that has minimal impact on code execution times.</span><span class="sxs-lookup"><span data-stu-id="8375e-113">It was built as a tracing technology that has minimal impact on code execution times.</span></span>
* <span data-ttu-id="8375e-114">**ETW tracing works seamlessly across local development environments and also real-world cluster setups.**</span><span class="sxs-lookup"><span data-stu-id="8375e-114">**ETW tracing works seamlessly across local development environments and also real-world cluster setups.**</span></span> <span data-ttu-id="8375e-115">This  means you don't have to rewrite your tracing code when you are ready to deploy your code to a real cluster.</span><span class="sxs-lookup"><span data-stu-id="8375e-115">This  means you don't have to rewrite your tracing code when you are ready to deploy your code to a real cluster.</span></span>
* <span data-ttu-id="8375e-116">**Service Fabric system code also uses ETW for internal tracing.**</span><span class="sxs-lookup"><span data-stu-id="8375e-116">**Service Fabric system code also uses ETW for internal tracing.**</span></span> <span data-ttu-id="8375e-117">This allows you to view your application traces interleaved with Service Fabric system traces.</span><span class="sxs-lookup"><span data-stu-id="8375e-117">This allows you to view your application traces interleaved with Service Fabric system traces.</span></span> <span data-ttu-id="8375e-118">It also helps you to more easily understand the sequences and interrelationships between your application code and events in the underlying system.</span><span class="sxs-lookup"><span data-stu-id="8375e-118">It also helps you to more easily understand the sequences and interrelationships between your application code and events in the underlying system.</span></span>
* <span data-ttu-id="8375e-119">**There is built-in support in Service Fabric Visual Studio tools to view ETW events.**</span><span class="sxs-lookup"><span data-stu-id="8375e-119">**There is built-in support in Service Fabric Visual Studio tools to view ETW events.**</span></span>

## <a name="view-service-fabric-system-events-in-visual-studio"></a><span data-ttu-id="8375e-120">View Service Fabric system events in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8375e-120">View Service Fabric system events in Visual Studio</span></span>
<span data-ttu-id="8375e-121">Service Fabric emits ETW events to help application developers understand what's happening in the platform.</span><span class="sxs-lookup"><span data-stu-id="8375e-121">Service Fabric emits ETW events to help application developers understand what's happening in the platform.</span></span> <span data-ttu-id="8375e-122">If you haven't already done so, go ahead and follow the steps in [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8375e-122">If you haven't already done so, go ahead and follow the steps in [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span> <span data-ttu-id="8375e-123">This information will help you get an application up and running with the Diagnostics Events Viewer showing the trace messages.</span><span class="sxs-lookup"><span data-stu-id="8375e-123">This information will help you get an application up and running with the Diagnostics Events Viewer showing the trace messages.</span></span>

1. <span data-ttu-id="8375e-124">If the diagnostics events window does not automatically show, Go to the **View** tab in Visual Studio, choose **Other Windows** and then **Diagnostic Events Viewer**.</span><span class="sxs-lookup"><span data-stu-id="8375e-124">If the diagnostics events window does not automatically show, Go to the **View** tab in Visual Studio, choose **Other Windows** and then **Diagnostic Events Viewer**.</span></span>
2. <span data-ttu-id="8375e-125">Each event has standard metadata information that tells you the node, application and service the event is coming from.</span><span class="sxs-lookup"><span data-stu-id="8375e-125">Each event has standard metadata information that tells you the node, application and service the event is coming from.</span></span> <span data-ttu-id="8375e-126">You can also filter the list of events by using the **Filter events** box at the top of the events window.</span><span class="sxs-lookup"><span data-stu-id="8375e-126">You can also filter the list of events by using the **Filter events** box at the top of the events window.</span></span> <span data-ttu-id="8375e-127">For example, you can filter on **Node Name** or **Service Name.**</span><span class="sxs-lookup"><span data-stu-id="8375e-127">For example, you can filter on **Node Name** or **Service Name.**</span></span> <span data-ttu-id="8375e-128">And when you're looking at event details, you can also pause by using the **Pause** button at the top of the events window and resume later without any loss of events.</span><span class="sxs-lookup"><span data-stu-id="8375e-128">And when you're looking at event details, you can also pause by using the **Pause** button at the top of the events window and resume later without any loss of events.</span></span>
   
   ![Visual Studio Diagnostics Events Viewer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-to-the-application-code"></a><span data-ttu-id="8375e-130">Add your own custom traces to the application code</span><span class="sxs-lookup"><span data-stu-id="8375e-130">Add your own custom traces to the application code</span></span>
<span data-ttu-id="8375e-131">The Service Fabric Visual Studio project templates contain sample code.</span><span class="sxs-lookup"><span data-stu-id="8375e-131">The Service Fabric Visual Studio project templates contain sample code.</span></span> <span data-ttu-id="8375e-132">The code shows how to add custom application code ETW traces that show up in the Visual Studio ETW viewer alongside system traces from Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8375e-132">The code shows how to add custom application code ETW traces that show up in the Visual Studio ETW viewer alongside system traces from Service Fabric.</span></span> <span data-ttu-id="8375e-133">The advantage of this method is that metadata is automatically added to traces, and the Visual Studio Diagnostic Events Viewer is already configured to display them.</span><span class="sxs-lookup"><span data-stu-id="8375e-133">The advantage of this method is that metadata is automatically added to traces, and the Visual Studio Diagnostic Events Viewer is already configured to display them.</span></span>

<span data-ttu-id="8375e-134">For projects created from the **service templates** (stateless or stateful) just search for the `RunAsync` implementation:</span><span class="sxs-lookup"><span data-stu-id="8375e-134">For projects created from the **service templates** (stateless or stateful) just search for the `RunAsync` implementation:</span></span>

1. <span data-ttu-id="8375e-135">The call to `ServiceEventSource.Current.ServiceMessage` in the `RunAsync` method shows an example of a custom ETW trace from the application code.</span><span class="sxs-lookup"><span data-stu-id="8375e-135">The call to `ServiceEventSource.Current.ServiceMessage` in the `RunAsync` method shows an example of a custom ETW trace from the application code.</span></span>
2. <span data-ttu-id="8375e-136">In the **ServiceEventSource.cs** file, you will find an overload for the `ServiceEventSource.ServiceMessage` method that should be used for high-frequency events due to performance reasons.</span><span class="sxs-lookup"><span data-stu-id="8375e-136">In the **ServiceEventSource.cs** file, you will find an overload for the `ServiceEventSource.ServiceMessage` method that should be used for high-frequency events due to performance reasons.</span></span>

<span data-ttu-id="8375e-137">For projects created from the **actor templates** (stateless or stateful):</span><span class="sxs-lookup"><span data-stu-id="8375e-137">For projects created from the **actor templates** (stateless or stateful):</span></span>

1. <span data-ttu-id="8375e-138">Open the **"ProjectName".cs** file where *ProjectName* is the name you chose for your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="8375e-138">Open the **"ProjectName".cs** file where *ProjectName* is the name you chose for your Visual Studio project.</span></span>  
2. <span data-ttu-id="8375e-139">Find the code `ActorEventSource.Current.ActorMessage(this, "Doing Work");` in the *DoWorkAsync* method.</span><span class="sxs-lookup"><span data-stu-id="8375e-139">Find the code `ActorEventSource.Current.ActorMessage(this, "Doing Work");` in the *DoWorkAsync* method.</span></span>  <span data-ttu-id="8375e-140">This is an example of a custom ETW trace written from application code.</span><span class="sxs-lookup"><span data-stu-id="8375e-140">This is an example of a custom ETW trace written from application code.</span></span>  
3. <span data-ttu-id="8375e-141">In file **ActorEventSource.cs**, you will find an overload for the `ActorEventSource.ActorMessage` method that should be used for high-frequency events due to performance reasons.</span><span class="sxs-lookup"><span data-stu-id="8375e-141">In file **ActorEventSource.cs**, you will find an overload for the `ActorEventSource.ActorMessage` method that should be used for high-frequency events due to performance reasons.</span></span>

<span data-ttu-id="8375e-142">After adding custom ETW tracing to your service code, you can build, deploy, and run the application again to see your event(s) in the Diagnostic Events Viewer.</span><span class="sxs-lookup"><span data-stu-id="8375e-142">After adding custom ETW tracing to your service code, you can build, deploy, and run the application again to see your event(s) in the Diagnostic Events Viewer.</span></span> <span data-ttu-id="8375e-143">If you debug the application with **F5**, the Diagnostic Events Viewer will open automatically.</span><span class="sxs-lookup"><span data-stu-id="8375e-143">If you debug the application with **F5**, the Diagnostic Events Viewer will open automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8375e-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="8375e-144">Next steps</span></span>
<span data-ttu-id="8375e-145">The same tracing code that you added to your application above for local diagnostics will work with tools that you can use to view these events when running your application on an Azure cluster.</span><span class="sxs-lookup"><span data-stu-id="8375e-145">The same tracing code that you added to your application above for local diagnostics will work with tools that you can use to view these events when running your application on an Azure cluster.</span></span> <span data-ttu-id="8375e-146">Check out these articles that discuss the different options for the tools and describe how you can set them up.</span><span class="sxs-lookup"><span data-stu-id="8375e-146">Check out these articles that discuss the different options for the tools and describe how you can set them up.</span></span>

* [<span data-ttu-id="8375e-147">How to collect logs with Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="8375e-147">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
* [<span data-ttu-id="8375e-148">Collect logs directly from service process</span><span class="sxs-lookup"><span data-stu-id="8375e-148">Collect logs directly from service process</span></span>](service-fabric-diagnostic-collect-logs-without-an-agent.md)

