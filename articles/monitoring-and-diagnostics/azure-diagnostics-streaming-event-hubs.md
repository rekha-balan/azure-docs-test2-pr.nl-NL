---
title: Streaming Azure Diagnostics data in the hot path using Event Hubs | Microsoft Docs
description: Configuring Azure Diagnostics with Event Hubs end to end, including guidance for common scenarios.
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: ''
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: robb
ms.openlocfilehash: 6247ad3aca3b195ca628257d66729d52bcf2f0e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549697"
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="85188-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span><span class="sxs-lookup"><span data-stu-id="85188-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="85188-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="85188-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="85188-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="85188-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="85188-106">Supported data types include:</span><span class="sxs-lookup"><span data-stu-id="85188-106">Supported data types include:</span></span>

* <span data-ttu-id="85188-107">Event Tracing for Windows (ETW) events</span><span class="sxs-lookup"><span data-stu-id="85188-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="85188-108">Performance counters</span><span class="sxs-lookup"><span data-stu-id="85188-108">Performance counters</span></span>
* <span data-ttu-id="85188-109">Windows event logs</span><span class="sxs-lookup"><span data-stu-id="85188-109">Windows event logs</span></span>
* <span data-ttu-id="85188-110">Application logs</span><span class="sxs-lookup"><span data-stu-id="85188-110">Application logs</span></span>
* <span data-ttu-id="85188-111">Azure Diagnostics infrastructure logs</span><span class="sxs-lookup"><span data-stu-id="85188-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="85188-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span><span class="sxs-lookup"><span data-stu-id="85188-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="85188-113">Guidance is also provided for the following common scenarios:</span><span class="sxs-lookup"><span data-stu-id="85188-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="85188-114">How to customize the logs and metrics that get sent to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="85188-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="85188-115">How to change configurations in each environment</span><span class="sxs-lookup"><span data-stu-id="85188-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="85188-116">How to view Event Hubs stream data</span><span class="sxs-lookup"><span data-stu-id="85188-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="85188-117">How to troubleshoot the connection</span><span class="sxs-lookup"><span data-stu-id="85188-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="85188-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="85188-118">Prerequisites</span></span>
<span data-ttu-id="85188-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85188-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="85188-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span><span class="sxs-lookup"><span data-stu-id="85188-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="85188-121">Visual Studio 2013 or later</span><span class="sxs-lookup"><span data-stu-id="85188-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="85188-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="85188-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="85188-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="85188-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="85188-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="85188-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="85188-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs]((../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="85188-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs]((../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="85188-126">Connect Azure Diagnostics to Event Hubs sink</span><span class="sxs-lookup"><span data-stu-id="85188-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="85188-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="85188-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="85188-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span><span class="sxs-lookup"><span data-stu-id="85188-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="85188-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span><span class="sxs-lookup"><span data-stu-id="85188-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```

<span data-ttu-id="85188-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span><span class="sxs-lookup"><span data-stu-id="85188-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="85188-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span><span class="sxs-lookup"><span data-stu-id="85188-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="85188-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span><span class="sxs-lookup"><span data-stu-id="85188-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="85188-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span><span class="sxs-lookup"><span data-stu-id="85188-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="85188-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span><span class="sxs-lookup"><span data-stu-id="85188-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="85188-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span><span class="sxs-lookup"><span data-stu-id="85188-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

```
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="" key="" endpoint="" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="9B3SwghJOGEUvXigc6zHPInl2iYxrgsKHZoy4nm9CUI=" />
</PrivateConfig>
```

The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace. Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions. <span data-ttu-id="85188-138">The **StorageAccount** is also declared in **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="85188-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="85188-139">There is no need to change values here if they are working.</span><span class="sxs-lookup"><span data-stu-id="85188-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="85188-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span><span class="sxs-lookup"><span data-stu-id="85188-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="85188-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span><span class="sxs-lookup"><span data-stu-id="85188-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="85188-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span><span class="sxs-lookup"><span data-stu-id="85188-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="85188-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span><span class="sxs-lookup"><span data-stu-id="85188-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="85188-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span><span class="sxs-lookup"><span data-stu-id="85188-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="85188-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="85188-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="85188-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span><span class="sxs-lookup"><span data-stu-id="85188-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="85188-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span><span class="sxs-lookup"><span data-stu-id="85188-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="85188-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span><span class="sxs-lookup"><span data-stu-id="85188-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="85188-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="85188-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="85188-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span><span class="sxs-lookup"><span data-stu-id="85188-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="85188-151">Systems that monitor alerts or autoscale rules are examples.</span><span class="sxs-lookup"><span data-stu-id="85188-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="85188-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span><span class="sxs-lookup"><span data-stu-id="85188-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="85188-153">The following are some example configurations.</span><span class="sxs-lookup"><span data-stu-id="85188-153">The following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
</PerformanceCounters>
```

<span data-ttu-id="85188-154">In the following example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="85188-154">In the following example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```

<span data-ttu-id="85188-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span><span class="sxs-lookup"><span data-stu-id="85188-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="85188-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span><span class="sxs-lookup"><span data-stu-id="85188-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

```
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```

<span data-ttu-id="85188-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span><span class="sxs-lookup"><span data-stu-id="85188-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="85188-158">Deploy and update a Cloud Services application and diagnostics config</span><span class="sxs-lookup"><span data-stu-id="85188-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="85188-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span><span class="sxs-lookup"><span data-stu-id="85188-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="85188-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span><span class="sxs-lookup"><span data-stu-id="85188-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="85188-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="85188-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="85188-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span><span class="sxs-lookup"><span data-stu-id="85188-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="85188-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span><span class="sxs-lookup"><span data-stu-id="85188-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="85188-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span><span class="sxs-lookup"><span data-stu-id="85188-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="85188-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span><span class="sxs-lookup"><span data-stu-id="85188-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="85188-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span><span class="sxs-lookup"><span data-stu-id="85188-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="85188-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span><span class="sxs-lookup"><span data-stu-id="85188-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="85188-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="85188-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="85188-169">View hot-path data</span><span class="sxs-lookup"><span data-stu-id="85188-169">View hot-path data</span></span>
<span data-ttu-id="85188-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span><span class="sxs-lookup"><span data-stu-id="85188-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="85188-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span><span class="sxs-lookup"><span data-stu-id="85188-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="85188-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span><span class="sxs-lookup"><span data-stu-id="85188-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="85188-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="85188-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="85188-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span><span class="sxs-lookup"><span data-stu-id="85188-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="85188-175">Troubleshoot Event Hubs sinks</span><span class="sxs-lookup"><span data-stu-id="85188-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="85188-176">The event hub does not show incoming or outgoing event activity as expected.</span><span class="sxs-lookup"><span data-stu-id="85188-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="85188-177">Check that your event hub is successfully provisioned.</span><span class="sxs-lookup"><span data-stu-id="85188-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="85188-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span><span class="sxs-lookup"><span data-stu-id="85188-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="85188-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span><span class="sxs-lookup"><span data-stu-id="85188-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="85188-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span><span class="sxs-lookup"><span data-stu-id="85188-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="85188-181">First, make sure that the event hub and configuration info is correct as explained previously.</span><span class="sxs-lookup"><span data-stu-id="85188-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="85188-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span><span class="sxs-lookup"><span data-stu-id="85188-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="85188-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span><span class="sxs-lookup"><span data-stu-id="85188-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="85188-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span><span class="sxs-lookup"><span data-stu-id="85188-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="85188-185">I tried the suggestions, and the event hub is still not working.</span><span class="sxs-lookup"><span data-stu-id="85188-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="85188-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="85188-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="85188-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span><span class="sxs-lookup"><span data-stu-id="85188-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="85188-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="85188-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="85188-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span><span class="sxs-lookup"><span data-stu-id="85188-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="85188-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="85188-190">Next steps</span></span>
<span data-ttu-id="85188-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="85188-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="85188-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span><span class="sxs-lookup"><span data-stu-id="85188-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount />
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="" key="" endpoint="" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="85188-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span><span class="sxs-lookup"><span data-stu-id="85188-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```
## <a name="next-steps"></a><span data-ttu-id="85188-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="85188-194">Next steps</span></span>
<span data-ttu-id="85188-195">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="85188-195">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="85188-196">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="85188-196">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="85188-197">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="85188-197">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="85188-198">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="85188-198">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png

