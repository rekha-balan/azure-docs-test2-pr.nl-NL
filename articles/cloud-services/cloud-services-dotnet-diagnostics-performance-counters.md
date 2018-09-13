---
title: Use Performance Counters in Azure Diagnostics | Microsoft Docs
description: Use performance counters in Azure cloud services or virtual machine to find bottlenecks and tune performance.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: 55623820a74b5226471d642e9b960480f25b4390
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554887"
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="1024c-103">Create and use performance counters in an Azure application</span><span class="sxs-lookup"><span data-stu-id="1024c-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="1024c-104">This article describes the benefits of and how to put performance counters into your Azure application.</span><span class="sxs-lookup"><span data-stu-id="1024c-104">This article describes the benefits of and how to put performance counters into your Azure application.</span></span> <span data-ttu-id="1024c-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span><span class="sxs-lookup"><span data-stu-id="1024c-105">You can use them to collect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="1024c-106">Performance counters available for Windows Server, IIS and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles and Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="1024c-106">Performance counters available for Windows Server, IIS and ASP.NET can also be collected and used to determine the health of your Azure web roles, worker roles and Virtual Machines.</span></span> <span data-ttu-id="1024c-107">You can also create and use custom performance counters.</span><span class="sxs-lookup"><span data-stu-id="1024c-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="1024c-108">You can examine performance counter data</span><span class="sxs-lookup"><span data-stu-id="1024c-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="1024c-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span><span class="sxs-lookup"><span data-stu-id="1024c-109">Directly on the application host with the Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="1024c-110">With System Center Operations Manager using the Azure Management Pack</span><span class="sxs-lookup"><span data-stu-id="1024c-110">With System Center Operations Manager using the Azure Management Pack</span></span>
3. <span data-ttu-id="1024c-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="1024c-111">With other monitoring tools that access the diagnostic data transferred to Azure storage.</span></span> <span data-ttu-id="1024c-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="1024c-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="1024c-113">For more information on monitoring the performance of your application in the [Azure classic portal](http://manage.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="1024c-113">For more information on monitoring the performance of your application in the [Azure classic portal](http://manage.azure.com/), see [How to Monitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="1024c-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="1024c-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques to troubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="1024c-115">Enable performance counter monitoring</span><span class="sxs-lookup"><span data-stu-id="1024c-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="1024c-116">Performance counters are not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="1024c-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="1024c-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span><span class="sxs-lookup"><span data-stu-id="1024c-117">Your application or a startup task must modify the default diagnostics agent configuration to include the specific performance counters that you wish to monitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="1024c-118">Performance counters available for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1024c-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="1024c-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span><span class="sxs-lookup"><span data-stu-id="1024c-119">Azure provides a subset of the performance counters available for Windows Server, IIS and the ASP.NET stack.</span></span> <span data-ttu-id="1024c-120">The following table lists some of the performance counters of particular interest for Azure applications.</span><span class="sxs-lookup"><span data-stu-id="1024c-120">The following table lists some of the performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="1024c-121">Counter Category: Object (Instance)</span><span class="sxs-lookup"><span data-stu-id="1024c-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="1024c-122">Counter Name</span><span class="sxs-lookup"><span data-stu-id="1024c-122">Counter Name</span></span> | <span data-ttu-id="1024c-123">Reference</span><span class="sxs-lookup"><span data-stu-id="1024c-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1024c-124">.NET CLR Exceptions(*Global*)</span><span class="sxs-lookup"><span data-stu-id="1024c-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="1024c-125"># Exceps Thrown / sec</span><span class="sxs-lookup"><span data-stu-id="1024c-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="1024c-126">Exception Performance Counters</span><span class="sxs-lookup"><span data-stu-id="1024c-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="1024c-127">.NET CLR Memory(*Global*)</span><span class="sxs-lookup"><span data-stu-id="1024c-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="1024c-128">% Time in GC</span><span class="sxs-lookup"><span data-stu-id="1024c-128">% Time in GC</span></span> |<span data-ttu-id="1024c-129">Memory Performance Counters</span><span class="sxs-lookup"><span data-stu-id="1024c-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="1024c-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-130">ASP.NET</span></span> |<span data-ttu-id="1024c-131">Application Restarts</span><span class="sxs-lookup"><span data-stu-id="1024c-131">Application Restarts</span></span> |<span data-ttu-id="1024c-132">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-133">ASP.NET</span></span> |<span data-ttu-id="1024c-134">Request Execution Time</span><span class="sxs-lookup"><span data-stu-id="1024c-134">Request Execution Time</span></span> |<span data-ttu-id="1024c-135">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-136">ASP.NET</span></span> |<span data-ttu-id="1024c-137">Requests Disconnected</span><span class="sxs-lookup"><span data-stu-id="1024c-137">Requests Disconnected</span></span> |<span data-ttu-id="1024c-138">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-139">ASP.NET</span></span> |<span data-ttu-id="1024c-140">Worker Process Restarts</span><span class="sxs-lookup"><span data-stu-id="1024c-140">Worker Process Restarts</span></span> |<span data-ttu-id="1024c-141">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-142">ASP.NET Applications(**Total**)</span><span class="sxs-lookup"><span data-stu-id="1024c-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="1024c-143">Requests Total</span><span class="sxs-lookup"><span data-stu-id="1024c-143">Requests Total</span></span> |<span data-ttu-id="1024c-144">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-145">ASP.NET Applications(**Total**)</span><span class="sxs-lookup"><span data-stu-id="1024c-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="1024c-146">Requests/Sec</span><span class="sxs-lookup"><span data-stu-id="1024c-146">Requests/Sec</span></span> |<span data-ttu-id="1024c-147">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-148">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="1024c-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="1024c-149">Request Execution Time</span><span class="sxs-lookup"><span data-stu-id="1024c-149">Request Execution Time</span></span> |<span data-ttu-id="1024c-150">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-151">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="1024c-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="1024c-152">Request Wait Time</span><span class="sxs-lookup"><span data-stu-id="1024c-152">Request Wait Time</span></span> |<span data-ttu-id="1024c-153">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-154">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="1024c-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="1024c-155">Requests Current</span><span class="sxs-lookup"><span data-stu-id="1024c-155">Requests Current</span></span> |<span data-ttu-id="1024c-156">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-157">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="1024c-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="1024c-158">Requests Queued</span><span class="sxs-lookup"><span data-stu-id="1024c-158">Requests Queued</span></span> |<span data-ttu-id="1024c-159">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-160">ASP.NET v4.0.30319</span><span class="sxs-lookup"><span data-stu-id="1024c-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="1024c-161">Requests Rejected</span><span class="sxs-lookup"><span data-stu-id="1024c-161">Requests Rejected</span></span> |<span data-ttu-id="1024c-162">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-163">Memory</span><span class="sxs-lookup"><span data-stu-id="1024c-163">Memory</span></span> |<span data-ttu-id="1024c-164">Available MBytes</span><span class="sxs-lookup"><span data-stu-id="1024c-164">Available MBytes</span></span> |<span data-ttu-id="1024c-165">Memory Performance Counters</span><span class="sxs-lookup"><span data-stu-id="1024c-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="1024c-166">Memory</span><span class="sxs-lookup"><span data-stu-id="1024c-166">Memory</span></span> |<span data-ttu-id="1024c-167">Committed Bytes</span><span class="sxs-lookup"><span data-stu-id="1024c-167">Committed Bytes</span></span> |<span data-ttu-id="1024c-168">Memory Performance Counters</span><span class="sxs-lookup"><span data-stu-id="1024c-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="1024c-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="1024c-169">Processor(_Total)</span></span> |<span data-ttu-id="1024c-170">% Processor Time</span><span class="sxs-lookup"><span data-stu-id="1024c-170">% Processor Time</span></span> |<span data-ttu-id="1024c-171">Performance Counters for ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1024c-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="1024c-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="1024c-172">TCPv4</span></span> |<span data-ttu-id="1024c-173">Connection Failures</span><span class="sxs-lookup"><span data-stu-id="1024c-173">Connection Failures</span></span> |<span data-ttu-id="1024c-174">TCP Object</span><span class="sxs-lookup"><span data-stu-id="1024c-174">TCP Object</span></span> |
| <span data-ttu-id="1024c-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="1024c-175">TCPv4</span></span> |<span data-ttu-id="1024c-176">Connections Established</span><span class="sxs-lookup"><span data-stu-id="1024c-176">Connections Established</span></span> |<span data-ttu-id="1024c-177">TCP Object</span><span class="sxs-lookup"><span data-stu-id="1024c-177">TCP Object</span></span> |
| <span data-ttu-id="1024c-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="1024c-178">TCPv4</span></span> |<span data-ttu-id="1024c-179">Connections Reset</span><span class="sxs-lookup"><span data-stu-id="1024c-179">Connections Reset</span></span> |<span data-ttu-id="1024c-180">TCP Object</span><span class="sxs-lookup"><span data-stu-id="1024c-180">TCP Object</span></span> |
| <span data-ttu-id="1024c-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="1024c-181">TCPv4</span></span> |<span data-ttu-id="1024c-182">Segments Sent/sec</span><span class="sxs-lookup"><span data-stu-id="1024c-182">Segments Sent/sec</span></span> |<span data-ttu-id="1024c-183">TCP Object</span><span class="sxs-lookup"><span data-stu-id="1024c-183">TCP Object</span></span> |
| <span data-ttu-id="1024c-184">Network Interface(\*)</span><span class="sxs-lookup"><span data-stu-id="1024c-184">Network Interface(\*)</span></span> |<span data-ttu-id="1024c-185">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="1024c-185">Bytes Received/sec</span></span> |<span data-ttu-id="1024c-186">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="1024c-186">Network Interface Object</span></span> |
| <span data-ttu-id="1024c-187">Network Interface(\*)</span><span class="sxs-lookup"><span data-stu-id="1024c-187">Network Interface(\*)</span></span> |<span data-ttu-id="1024c-188">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="1024c-188">Bytes Sent/sec</span></span> |<span data-ttu-id="1024c-189">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="1024c-189">Network Interface Object</span></span> |
| <span data-ttu-id="1024c-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="1024c-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="1024c-191">Bytes Received/sec</span><span class="sxs-lookup"><span data-stu-id="1024c-191">Bytes Received/sec</span></span> |<span data-ttu-id="1024c-192">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="1024c-192">Network Interface Object</span></span> |
| <span data-ttu-id="1024c-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="1024c-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="1024c-194">Bytes Sent/sec</span><span class="sxs-lookup"><span data-stu-id="1024c-194">Bytes Sent/sec</span></span> |<span data-ttu-id="1024c-195">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="1024c-195">Network Interface Object</span></span> |
| <span data-ttu-id="1024c-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span><span class="sxs-lookup"><span data-stu-id="1024c-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="1024c-197">Bytes Total/sec</span><span class="sxs-lookup"><span data-stu-id="1024c-197">Bytes Total/sec</span></span> |<span data-ttu-id="1024c-198">Network Interface Object</span><span class="sxs-lookup"><span data-stu-id="1024c-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-to-your-application"></a><span data-ttu-id="1024c-199">Create and add custom performance counters to your application</span><span class="sxs-lookup"><span data-stu-id="1024c-199">Create and add custom performance counters to your application</span></span>
<span data-ttu-id="1024c-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span><span class="sxs-lookup"><span data-stu-id="1024c-200">Azure has support to create and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="1024c-201">The counters may be used to track and monitor application-specific behavior.</span><span class="sxs-lookup"><span data-stu-id="1024c-201">The counters may be used to track and monitor application-specific behavior.</span></span> <span data-ttu-id="1024c-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span><span class="sxs-lookup"><span data-stu-id="1024c-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="1024c-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span><span class="sxs-lookup"><span data-stu-id="1024c-203">Code that makes changes to custom performance counters must have elevated permissions to run.</span></span> <span data-ttu-id="1024c-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span><span class="sxs-lookup"><span data-stu-id="1024c-204">If the code is in a web role or worker role, the role must include the tag <Runtime executionContext="elevated" /> in the ServiceDefinition.csdef file for the role to initialize properly.</span></span>
> 
> 

<span data-ttu-id="1024c-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span><span class="sxs-lookup"><span data-stu-id="1024c-205">You can send custom performance counter data to Azure storage using the diagnostics agent.</span></span>

<span data-ttu-id="1024c-206">The standard performance counter data is generated by the Azure processes.</span><span class="sxs-lookup"><span data-stu-id="1024c-206">The standard performance counter data is generated by the Azure processes.</span></span> <span data-ttu-id="1024c-207">Custom performance counter data must be created by your web role or worker role application.</span><span class="sxs-lookup"><span data-stu-id="1024c-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="1024c-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span><span class="sxs-lookup"><span data-stu-id="1024c-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on the types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="1024c-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span><span class="sxs-lookup"><span data-stu-id="1024c-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="1024c-210">Store and view performance counter data</span><span class="sxs-lookup"><span data-stu-id="1024c-210">Store and view performance counter data</span></span>
<span data-ttu-id="1024c-211">Azure caches performance counter data with other diagnostic information.</span><span class="sxs-lookup"><span data-stu-id="1024c-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="1024c-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span><span class="sxs-lookup"><span data-stu-id="1024c-212">This data is available for remote monitoring while the role instance is running using remote desktop access to view tools such as Performance Monitor.</span></span> <span data-ttu-id="1024c-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="1024c-213">To persist the data outside of the role instance, the diagnostics agent must transfer the data to Azure storage.</span></span> <span data-ttu-id="1024c-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="1024c-214">The size limit of the cached performance counter data can be configured in the diagnostics agent, or it may be configured to be part of a shared limit for all the diagnostic data.</span></span> <span data-ttu-id="1024c-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="1024c-215">For more information about setting the buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="1024c-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span><span class="sxs-lookup"><span data-stu-id="1024c-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up the diagnostics agent to transfer data to a storage account.</span></span>

<span data-ttu-id="1024c-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span><span class="sxs-lookup"><span data-stu-id="1024c-217">Each configured performance counter instance is recorded at a specified sampling rate, and the sampled data is transferred to the storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="1024c-218">Automatic transfers may be scheduled as often as once per minute.</span><span class="sxs-lookup"><span data-stu-id="1024c-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="1024c-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span><span class="sxs-lookup"><span data-stu-id="1024c-219">Performance counter data transferred by the diagnostics agent is stored in a table, WADPerformanceCountersTable, in the storage account.</span></span> <span data-ttu-id="1024c-220">This table may be accessed and queried with standard Azure storage API methods.</span><span class="sxs-lookup"><span data-stu-id="1024c-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="1024c-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span><span class="sxs-lookup"><span data-stu-id="1024c-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from the WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="1024c-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span><span class="sxs-lookup"><span data-stu-id="1024c-222">Depending on the diagnostics agent transfer frequency and queue latency, the most recent performance counter data in the storage account may be several minutes out of date.</span></span>
> 
> 

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="1024c-223">Enable performance counters using diagnostics configuration file</span><span class="sxs-lookup"><span data-stu-id="1024c-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="1024c-224">Use the following procedure to enable performance counters in your Azure application.</span><span class="sxs-lookup"><span data-stu-id="1024c-224">Use the following procedure to enable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1024c-225">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1024c-225">Prerequisites</span></span>
<span data-ttu-id="1024c-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span><span class="sxs-lookup"><span data-stu-id="1024c-226">This section assumes that you have imported the Diagnostics monitor into your application and added the diagnostics configuration file to your Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="1024c-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span><span class="sxs-lookup"><span data-stu-id="1024c-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="1024c-228">Step 1: Collect and store data from performance counters</span><span class="sxs-lookup"><span data-stu-id="1024c-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="1024c-229">After you have added the diagnostics file to your Visual Studio solution you can configure the collection and storage of performance counter data in a Azure application.</span><span class="sxs-lookup"><span data-stu-id="1024c-229">After you have added the diagnostics file to your Visual Studio solution you can configure the collection and storage of performance counter data in a Azure application.</span></span> <span data-ttu-id="1024c-230">This is done by adding performance counters to the diagnostics file.</span><span class="sxs-lookup"><span data-stu-id="1024c-230">This is done by adding performance counters to the diagnostics file.</span></span> <span data-ttu-id="1024c-231">Diagnostics data, including performance counters, is first collected on the instance.</span><span class="sxs-lookup"><span data-stu-id="1024c-231">Diagnostics data, including performance counters, is first collected on the instance.</span></span> <span data-ttu-id="1024c-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span><span class="sxs-lookup"><span data-stu-id="1024c-232">The data is then persisted to the WADPerformanceCountersTable table in the Azure Table service, so you will also need to specify the storage account in your application.</span></span> <span data-ttu-id="1024c-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span><span class="sxs-lookup"><span data-stu-id="1024c-233">If you're testing your application locally in the Compute Emulator, you can also store diagnostics data locally in the Storage Emulator.</span></span> <span data-ttu-id="1024c-234">Before you store diagnostics data you must first go to the [Azure classic portal](http://manage.windowsazure.com/) and create a storage account.</span><span class="sxs-lookup"><span data-stu-id="1024c-234">Before you store diagnostics data you must first go to the [Azure classic portal](http://manage.windowsazure.com/) and create a storage account.</span></span> <span data-ttu-id="1024c-235">A best practice is to locate your storage account in the same geo-location as your Azure application in order to avoid paying external bandwidth costs and to reduce latency.</span><span class="sxs-lookup"><span data-stu-id="1024c-235">A best practice is to locate your storage account in the same geo-location as your Azure application in order to avoid paying external bandwidth costs and to reduce latency.</span></span>

### <a name="add-performance-counters-to-the-diagnostics-file"></a><span data-ttu-id="1024c-236">Add performance counters to the diagnostics file</span><span class="sxs-lookup"><span data-stu-id="1024c-236">Add performance counters to the diagnostics file</span></span>
<span data-ttu-id="1024c-237">There are many counters you can use.</span><span class="sxs-lookup"><span data-stu-id="1024c-237">There are many counters you can use.</span></span> <span data-ttu-id="1024c-238">The following example shows several performance counters that are recommended for web and worker role monitoring.</span><span class="sxs-lookup"><span data-stu-id="1024c-238">The following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="1024c-239">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span><span class="sxs-lookup"><span data-stu-id="1024c-239">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use the Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use the Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="1024c-240">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span><span class="sxs-lookup"><span data-stu-id="1024c-240">The bufferQuotaInMB attribute, which specifies the maximum amount of file system storage that is available for the data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="1024c-241">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="1024c-241">The default is 0.</span></span> <span data-ttu-id="1024c-242">When the quota is reached, the oldest data is deleted as new data is added.</span><span class="sxs-lookup"><span data-stu-id="1024c-242">When the quota is reached, the oldest data is deleted as new data is added.</span></span> <span data-ttu-id="1024c-243">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span><span class="sxs-lookup"><span data-stu-id="1024c-243">The sum of all the bufferQuotaInMB properties must be greater than the value of the OverallQuotaInMB attribute.</span></span> <span data-ttu-id="1024c-244">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="1024c-244">For a more detailed discussion of determining how much storage will be required for the collection of diagnostics data, see the Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="1024c-245">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="1024c-245">The scheduledTransferPeriod attribute, which specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span> <span data-ttu-id="1024c-246">In the following examples it is set to PT30M (30 minutes).</span><span class="sxs-lookup"><span data-stu-id="1024c-246">In the following examples it is set to PT30M (30 minutes).</span></span> <span data-ttu-id="1024c-247">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span><span class="sxs-lookup"><span data-stu-id="1024c-247">Setting the transfer period to a small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="1024c-248">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span><span class="sxs-lookup"><span data-stu-id="1024c-248">The scheduled transfer period should be small enough to ensure that diagnostic data is not overwritten on the instance, but large enough that it will not impact the performance of your application.</span></span>

<span data-ttu-id="1024c-249">The counterSpecifier attribute specifies the performance counter to collect.The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="1024c-249">The counterSpecifier attribute specifies the performance counter to collect.The sampleRate attribute specifies the rate at which the performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="1024c-250">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span><span class="sxs-lookup"><span data-stu-id="1024c-250">Once you've added the performance counters that you want to collect, save your changes to the diagnostics file.</span></span> <span data-ttu-id="1024c-251">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span><span class="sxs-lookup"><span data-stu-id="1024c-251">Next, you need to specify the storage account that the diagnostics data will be persisted to.</span></span>

### <a name="specify-the-storage-account"></a><span data-ttu-id="1024c-252">Specify the storage account</span><span class="sxs-lookup"><span data-stu-id="1024c-252">Specify the storage account</span></span>
<span data-ttu-id="1024c-253">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="1024c-253">To persist your diagnostics information to your Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="1024c-254">For Azure SDK 2.5 the Storage Account can be specified in the diagnostics.wadcfgx file.</span><span class="sxs-lookup"><span data-stu-id="1024c-254">For Azure SDK 2.5 the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="1024c-255">These instructions only apply to Azure SDK 2.4 and below.</span><span class="sxs-lookup"><span data-stu-id="1024c-255">These instructions only apply to Azure SDK 2.4 and below.</span></span> <span data-ttu-id="1024c-256">For Azure SDK 2.5 the Storage Account can be specified in the diagnostics.wadcfgx file.</span><span class="sxs-lookup"><span data-stu-id="1024c-256">For Azure SDK 2.5 the Storage Account can be specified in the diagnostics.wadcfgx file.</span></span>
> 
> 

<span data-ttu-id="1024c-257">To set the connection strings:</span><span class="sxs-lookup"><span data-stu-id="1024c-257">To set the connection strings:</span></span>

1. <span data-ttu-id="1024c-258">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span><span class="sxs-lookup"><span data-stu-id="1024c-258">Open the ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set the connection string for your storage.</span></span> <span data-ttu-id="1024c-259">The *AccountName* and *AccountKey* values are found in the Azure classic portal in the storage account dashboard, under Manage Keys.</span><span class="sxs-lookup"><span data-stu-id="1024c-259">The *AccountName* and *AccountKey* values are found in the Azure classic portal in the storage account dashboard, under Manage Keys.</span></span>
  
    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="1024c-260">Save the ServiceConfiguration.Cloud.cscfg file.</span><span class="sxs-lookup"><span data-stu-id="1024c-260">Save the ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="1024c-261">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span><span class="sxs-lookup"><span data-stu-id="1024c-261">Open the ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set to true.</span></span>
   
    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="1024c-262">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span><span class="sxs-lookup"><span data-stu-id="1024c-262">Now that the connection strings are set, your application will persist diagnostics data to your storage account when your application is deployed.</span></span>
4. <span data-ttu-id="1024c-263">Save and build your project, then deploy your application.</span><span class="sxs-lookup"><span data-stu-id="1024c-263">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="1024c-264">Step 2: (Optional) Create custom performance counters</span><span class="sxs-lookup"><span data-stu-id="1024c-264">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="1024c-265">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span><span class="sxs-lookup"><span data-stu-id="1024c-265">In addition to the pre-defined performance counters, you can add your own custom performance counters to monitor web or worker roles.</span></span> <span data-ttu-id="1024c-266">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span><span class="sxs-lookup"><span data-stu-id="1024c-266">Custom performance counters may be used to track and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="1024c-267">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span><span class="sxs-lookup"><span data-stu-id="1024c-267">The Azure diagnostics agent refreshes the performance counter configuration from the .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="1024c-268">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span><span class="sxs-lookup"><span data-stu-id="1024c-268">If you create custom performance counters in the OnStart method and your startup tasks take longer than one minute to execute, your custom performance counters will not have been created when the Azure Diagnostics agent tries to load them.</span></span>  <span data-ttu-id="1024c-269">In this scenario you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span><span class="sxs-lookup"><span data-stu-id="1024c-269">In this scenario you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="1024c-270">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span><span class="sxs-lookup"><span data-stu-id="1024c-270">To resolve this issue, create the performance counters in a startup task or move some of your startup task work to the OnStart method after creating the performance counters.</span></span>

<span data-ttu-id="1024c-271">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span><span class="sxs-lookup"><span data-stu-id="1024c-271">Perform the following steps to create a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="1024c-272">Open the service definition file (CSDEF) for your application.</span><span class="sxs-lookup"><span data-stu-id="1024c-272">Open the service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="1024c-273">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span><span class="sxs-lookup"><span data-stu-id="1024c-273">Add the Runtime element to the WebRole or WorkerRole element to allow execution with elevated privileges:</span></span>
   
    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="1024c-274">Save the file.</span><span class="sxs-lookup"><span data-stu-id="1024c-274">Save the file.</span></span>
4. <span data-ttu-id="1024c-275">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="1024c-275">Open the diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add the following to the DiagnosticMonitorConfiguration</span></span> 
   
    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="1024c-276">Save the file.</span><span class="sxs-lookup"><span data-stu-id="1024c-276">Save the file.</span></span>
6. <span data-ttu-id="1024c-277">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span><span class="sxs-lookup"><span data-stu-id="1024c-277">Create the custom performance counter category in the OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="1024c-278">The following C# example creates a custom category, if it does not already exist:</span><span class="sxs-lookup"><span data-stu-id="1024c-278">The following C# example creates a custom category, if it does not already exist:</span></span>
   
    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();
   
         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);
   
         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);
   
         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }
   
    return base.OnStart();
    }
    ```
7. <span data-ttu-id="1024c-279">Update the counters within your application.</span><span class="sxs-lookup"><span data-stu-id="1024c-279">Update the counters within your application.</span></span> <span data-ttu-id="1024c-280">The following example updates a custom performance counter on Button1_Click events:</span><span class="sxs-lookup"><span data-stu-id="1024c-280">The following example updates a custom performance counter on Button1_Click events:</span></span>
   
    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="1024c-281">Save the file.</span><span class="sxs-lookup"><span data-stu-id="1024c-281">Save the file.</span></span>  

<span data-ttu-id="1024c-282">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span><span class="sxs-lookup"><span data-stu-id="1024c-282">Custom performance counter data will now be collected by the Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="1024c-283">Step 3: Query performance counter data</span><span class="sxs-lookup"><span data-stu-id="1024c-283">Step 3: Query performance counter data</span></span>
<span data-ttu-id="1024c-284">Once your application is deployed and running the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="1024c-284">Once your application is deployed and running the Diagnostics monitor will begin collecting performance counters and persisting that data to Azure storage.</span></span> <span data-ttu-id="1024c-285">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span><span class="sxs-lookup"><span data-stu-id="1024c-285">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata to view the performance counters data in the WADPerformanceCountersTable table.</span></span> <span data-ttu-id="1024c-286">You can also programatically query the Table service using [C#](../storage/storage-dotnet-how-to-use-tables.md),  [Java](../storage/storage-java-how-to-use-table-storage.md),  [Node.js](../storage/storage-nodejs-how-to-use-table-storage.md), [Python](../storage/storage-python-how-to-use-table-storage.md), [Ruby](../storage/storage-ruby-how-to-use-table-storage.md), or [PHP](../storage/storage-php-how-to-use-table-storage.md).</span><span class="sxs-lookup"><span data-stu-id="1024c-286">You can also programatically query the Table service using [C#](../storage/storage-dotnet-how-to-use-tables.md),  [Java](../storage/storage-java-how-to-use-table-storage.md),  [Node.js](../storage/storage-nodejs-how-to-use-table-storage.md), [Python](../storage/storage-python-how-to-use-table-storage.md), [Ruby](../storage/storage-ruby-how-to-use-table-storage.md), or [PHP](../storage/storage-php-how-to-use-table-storage.md).</span></span>

<span data-ttu-id="1024c-287">The following C# example shows a simple query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span><span class="sxs-lookup"><span data-stu-id="1024c-287">The following C# example shows a simple query against the WADPerformanceCountersTable table and saves the diagnostics data to a CSV file.</span></span> <span data-ttu-id="1024c-288">Once the performance counters are saved to a CSV file you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span><span class="sxs-lookup"><span data-stu-id="1024c-288">Once the performance counters are saved to a CSV file you can use the graphing capabilities in Microsoft Excel or some other tool to visualize the data.</span></span> <span data-ttu-id="1024c-289">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span><span class="sxs-lookup"><span data-stu-id="1024c-289">Be sure to add a reference to Microsoft.WindowsAzure.Storage.dll, which is included in the Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="1024c-290">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span><span class="sxs-lookup"><span data-stu-id="1024c-290">The assembly is installed to the %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get the connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using the Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use the CloudConfigurationManager type
// to retrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store the connection string in your web.config or app.config file.
// Use the ConfigurationManager type to retrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference to the storage account using the connection string.  You can also use the development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create the table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute the table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process the query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="1024c-291">Entities map to C# objects using a custom class derived from **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="1024c-291">Entities map to C# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="1024c-292">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span><span class="sxs-lookup"><span data-stu-id="1024c-292">The following code defines an entity class that represents a performance counter in the **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="1024c-293">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1024c-293">Next Steps</span></span>
[<span data-ttu-id="1024c-294">View additional articles on Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="1024c-294">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
