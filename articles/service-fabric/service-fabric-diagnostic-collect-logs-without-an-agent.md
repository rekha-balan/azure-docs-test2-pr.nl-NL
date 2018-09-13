---
title: Collect logs directly from an Azure Service Fabric service process | Microsoft Azure
description: Describes Service Fabric applications can send logs directly to a central location like Azure Application Insights or Elasticsearch, without relying on Azure Diagnostics agent.
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: ''
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
ms.openlocfilehash: 5c0c35cf0524b1bc6ccd89d8bf83c08189854281
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551861"
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="2cd9a-103">Collect logs directly from an Azure Service Fabric service process</span><span class="sxs-lookup"><span data-stu-id="2cd9a-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="2cd9a-104">In-process log collection</span><span class="sxs-lookup"><span data-stu-id="2cd9a-104">In-process log collection</span></span>
<span data-ttu-id="2cd9a-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="2cd9a-106">If not, an alternative is to have services send their logs directly to a central location.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="2cd9a-107">This process is known as **in-process log collection** and has several potential advantages:</span><span class="sxs-lookup"><span data-stu-id="2cd9a-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="2cd9a-108">*Easy configuration and deployment*</span><span class="sxs-lookup"><span data-stu-id="2cd9a-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="2cd9a-109">The configuration of diagnostic data collection is just part of the service configuration.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="2cd9a-110">It is easy to always keep it "in sync" with the rest of the application.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="2cd9a-111">Per-application or per-service configuration is easily achievable.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="2cd9a-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="2cd9a-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="2cd9a-114">*Flexibility*</span><span class="sxs-lookup"><span data-stu-id="2cd9a-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="2cd9a-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="2cd9a-116">New destinations can be added as desired.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="2cd9a-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="2cd9a-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="2cd9a-119">Some agents are extensible.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-119">Some agents are extensible.</span></span>

* <span data-ttu-id="2cd9a-120">*Access to internal application data and context*</span><span class="sxs-lookup"><span data-stu-id="2cd9a-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="2cd9a-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="2cd9a-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="2cd9a-123">This mechanism could impose additional limitations.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="2cd9a-124">It is possible to combine and benefit from both collection methods.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="2cd9a-125">Indeed, it might be the best solution for many applications.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="2cd9a-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="2cd9a-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="2cd9a-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="2cd9a-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="2cd9a-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="2cd9a-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="2cd9a-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="2cd9a-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="2cd9a-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="2cd9a-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="2cd9a-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="2cd9a-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="2cd9a-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="2cd9a-137">Adding EventFlow library to a Service Fabric service project</span><span class="sxs-lookup"><span data-stu-id="2cd9a-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="2cd9a-138">EventFlow binaries are available as a set of NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="2cd9a-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span><span class="sxs-lookup"><span data-stu-id="2cd9a-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="2cd9a-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="2cd9a-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![EventFlow NuGet packages in Visual Studio NuGet package manager UI][1]

<span data-ttu-id="2cd9a-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="2cd9a-143">Add the following packages:</span><span class="sxs-lookup"><span data-stu-id="2cd9a-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Input.EventSource` 
    * <span data-ttu-id="2cd9a-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="2cd9a-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` 
    * <span data-ttu-id="2cd9a-145">(we are going to send the logs to an Azure Application Insights resource)</span><span class="sxs-lookup"><span data-stu-id="2cd9a-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="2cd9a-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span><span class="sxs-lookup"><span data-stu-id="2cd9a-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="2cd9a-147">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-147">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="2cd9a-148">Make sure you set the appropriate target framework in project properties before installing this package.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="2cd9a-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="2cd9a-150">Configuring and enabling log collection</span><span class="sxs-lookup"><span data-stu-id="2cd9a-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="2cd9a-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="2cd9a-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="2cd9a-153">The file name is `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="2cd9a-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="2cd9a-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="2cd9a-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="2cd9a-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="2cd9a-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="2cd9a-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> <span data-ttu-id="2cd9a-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="2cd9a-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="2cd9a-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="2cd9a-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="2cd9a-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="2cd9a-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="2cd9a-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="2cd9a-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="2cd9a-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="2cd9a-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span><span class="sxs-lookup"><span data-stu-id="2cd9a-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is the entry point of the service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="2cd9a-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="2cd9a-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="2cd9a-169">Verification</span><span class="sxs-lookup"><span data-stu-id="2cd9a-169">Verification</span></span>
<span data-ttu-id="2cd9a-170">Start your service and observe the Debug output window in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="2cd9a-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="2cd9a-172">Open a web browser and navigate go to your Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="2cd9a-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="2cd9a-173">Open "Search" tab (at the top of the default "Overview" blade).</span><span class="sxs-lookup"><span data-stu-id="2cd9a-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="2cd9a-174">After a short delay you should start seeing your traces in the Application Insights portal:</span><span class="sxs-lookup"><span data-stu-id="2cd9a-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![Application Insights portal showing logs from a Service Fabric application][2]

## <a name="next-steps"></a><span data-ttu-id="2cd9a-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="2cd9a-176">Next steps</span></span>
* [<span data-ttu-id="2cd9a-177">Learn more about diagnosing and monitoring a Service Fabric service</span><span class="sxs-lookup"><span data-stu-id="2cd9a-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="2cd9a-178">EventFlow documentation</span><span class="sxs-lookup"><span data-stu-id="2cd9a-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png

