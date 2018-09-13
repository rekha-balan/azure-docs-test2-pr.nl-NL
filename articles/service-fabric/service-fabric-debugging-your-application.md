---
title: Debug your application in Visual Studio | Microsoft Docs
description: Improve the reliability and performance of your services by developing and debugging them in Visual Studio on a local development cluster.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/07/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: b5abd328d5a19cabacbcf7eb53c5228dfcc8bcdc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550440"
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="6115a-103">Debug your Service Fabric application by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6115a-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="6115a-106">Debug a local Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="6115a-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="6115a-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span><span class="sxs-lookup"><span data-stu-id="6115a-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="6115a-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span><span class="sxs-lookup"><span data-stu-id="6115a-108">Visual Studio 2017 or Visual Studio 2015 can deploy the application to the local cluster and automatically connect the debugger to all instances of your application.</span></span>

1. <span data-ttu-id="6115a-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6115a-109">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="6115a-110">Press **F5** or click **Debug** > **Start Debugging**.</span><span class="sxs-lookup"><span data-stu-id="6115a-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Start debugging an application][startdebugging]
3. <span data-ttu-id="6115a-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span><span class="sxs-lookup"><span data-stu-id="6115a-112">Set breakpoints in your code and step through the application by clicking commands in the **Debug** menu.</span></span>
   
   > [!NOTE]
   > Visual Studio attaches to all instances of your application. While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions. Try disabling the breakpoints after they're hit, by making each breakpoint conditional on the thread ID or by using diagnostic events.
   > 
   > 
4. <span data-ttu-id="6115a-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real-time.</span><span class="sxs-lookup"><span data-stu-id="6115a-116">The **Diagnostic Events** window will automatically open so you can view diagnostic events in real-time.</span></span>
   
    ![View diagnostic events in real time][diagnosticevents]
5. <span data-ttu-id="6115a-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="6115a-118">You can also open the **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="6115a-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span><span class="sxs-lookup"><span data-stu-id="6115a-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Open the diagnostic events window][viewdiagnosticevents]
   
    <span data-ttu-id="6115a-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span><span class="sxs-lookup"><span data-stu-id="6115a-121">If you want to filter your traces to a specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="6115a-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span><span class="sxs-lookup"><span data-stu-id="6115a-122">The diagnostic events can be seen in the automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="6115a-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real-time.</span><span class="sxs-lookup"><span data-stu-id="6115a-123">The **Diagnostic Events** window supports filtering, pausing, and inspecting events in real-time.</span></span>  <span data-ttu-id="6115a-124">The filter is a simple string search of the event message, including its contents.</span><span class="sxs-lookup"><span data-stu-id="6115a-124">The filter is a simple string search of the event message, including its contents.</span></span>
   
    ![Filter, pause and resume, or inspect events in real-time][diagnosticeventsactions]
8. <span data-ttu-id="6115a-126">Debugging services is like debugging any other application.</span><span class="sxs-lookup"><span data-stu-id="6115a-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="6115a-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span><span class="sxs-lookup"><span data-stu-id="6115a-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="6115a-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span><span class="sxs-lookup"><span data-stu-id="6115a-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="6115a-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span><span class="sxs-lookup"><span data-stu-id="6115a-129">This means that you can use the Results View in Visual Studio while debugging to see what you've stored inside.</span></span> <span data-ttu-id="6115a-130">Simply set a breakpoint anywhere in your code.</span><span class="sxs-lookup"><span data-stu-id="6115a-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Start debugging an application][breakpoint]

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="6115a-132">Debug a remote Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="6115a-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="6115a-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6115a-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able to remotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> The feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Remote debugging is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.
> 
> 

1. <span data-ttu-id="6115a-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span><span class="sxs-lookup"><span data-stu-id="6115a-136">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Enable remote debugging][enableremotedebugging]
   
    <span data-ttu-id="6115a-138">This will kick-off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span><span class="sxs-lookup"><span data-stu-id="6115a-138">This will kick-off the process of enabling the remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="6115a-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span><span class="sxs-lookup"><span data-stu-id="6115a-139">Right-click the cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Attach debugger][attachdebugger]
3. <span data-ttu-id="6115a-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span><span class="sxs-lookup"><span data-stu-id="6115a-141">In the **Attach to process** dialog, choose the process you want to debug, and click **Attach**</span></span>
   
    ![Choose process][chooseprocess]
   
    <span data-ttu-id="6115a-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span><span class="sxs-lookup"><span data-stu-id="6115a-143">The name of the process you want to attach to, equals the name of your service project assembly name.</span></span>
   
    <span data-ttu-id="6115a-144">The debugger will attach to all nodes running the process.</span><span class="sxs-lookup"><span data-stu-id="6115a-144">The debugger will attach to all nodes running the process.</span></span>
   
   * <span data-ttu-id="6115a-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span><span class="sxs-lookup"><span data-stu-id="6115a-145">In the case where you are debugging a stateless service, all instances of the service on all nodes are part of the debug session.</span></span>
   * <span data-ttu-id="6115a-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span><span class="sxs-lookup"><span data-stu-id="6115a-146">If you are debugging a stateful service, only the primary replica of any partition will be active and therefore caught by the debugger.</span></span> <span data-ttu-id="6115a-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span><span class="sxs-lookup"><span data-stu-id="6115a-147">If the primary replica moves during the debug session, the processing of that replica will still be part of the debug session.</span></span>
   * <span data-ttu-id="6115a-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span><span class="sxs-lookup"><span data-stu-id="6115a-148">In order to only catch relevant partitions or instances of a given service, you can use conditional breakpoints to only break a specific partition or instance.</span></span>
     
     ![Conditional breakpoint][conditionalbreakpoint]
     
     > [!NOTE]
     > Currently we do not support debugging a Service Fabric cluster with multiple instances of the same service executable name.
     > 
     > 
4. <span data-ttu-id="6115a-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span><span class="sxs-lookup"><span data-stu-id="6115a-151">Once you finish debugging your application, you can disable the remote debugging extension by right-clicking the cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Disable remote debugging][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="6115a-153">Streaming traces from a remote cluster node</span><span class="sxs-lookup"><span data-stu-id="6115a-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="6115a-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6115a-154">You are also able to stream traces directly from a remote cluster node to Visual Studio.</span></span> <span data-ttu-id="6115a-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span><span class="sxs-lookup"><span data-stu-id="6115a-155">This feature allows you to stream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).
> This feature only supports clusters running in Azure.
> 
> 

<!-- -->
> [!WARNING]
> Streaming traces is meant for dev/test scenarios and not to be used in production environments, because of the impact on the running applications.
> In a production scenario, you should rely on forwarding events using Azure Diagnostics.
> 
> 

1. <span data-ttu-id="6115a-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span><span class="sxs-lookup"><span data-stu-id="6115a-160">Navigate to your cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Enable remote streaming traces][enablestreamingtraces]
   
    <span data-ttu-id="6115a-162">This will kick-off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span><span class="sxs-lookup"><span data-stu-id="6115a-162">This will kick-off the process of enabling the streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="6115a-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span><span class="sxs-lookup"><span data-stu-id="6115a-163">Expand the **Nodes** element in **Cloud Explorer**, right-click the node you want to stream traces from and choose **View Streaming Traces**</span></span>
   
    ![View remote streaming traces][viewremotestreamingtraces]
   
    <span data-ttu-id="6115a-165">Repeat step 2 for as many nodes as you want to see traces from.</span><span class="sxs-lookup"><span data-stu-id="6115a-165">Repeat step 2 for as many nodes as you want to see traces from.</span></span> <span data-ttu-id="6115a-166">Each nodes stream will show up in a dedicated window.</span><span class="sxs-lookup"><span data-stu-id="6115a-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="6115a-167">You are now able to see the traces emitted by Service Fabric, and your services.</span><span class="sxs-lookup"><span data-stu-id="6115a-167">You are now able to see the traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="6115a-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span><span class="sxs-lookup"><span data-stu-id="6115a-168">If you want to filter the events to only show a specific application, simply type in the name of the application in the filter.</span></span>
   
    ![Viewing streaming traces][viewingstreamingtraces]
3. <span data-ttu-id="6115a-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span><span class="sxs-lookup"><span data-stu-id="6115a-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking the cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Disable remote streaming traces][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="6115a-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="6115a-172">Next steps</span></span>
* <span data-ttu-id="6115a-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6115a-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="6115a-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="6115a-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-debugging-your-application/disablestreamingtraces.png














