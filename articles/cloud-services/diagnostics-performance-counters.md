---
title: Collect on Performance Counters in Azure Cloud Services | Microsoft Docs
description: Learn how to discover, use, and create performance counters in Cloud Services with Azure Diagnostics and Application Insights.
services: cloud-services
documentationcenter: .net
author: jpconnock
manager: timlt
editor: ''
ms.assetid: ''
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/18
ms.author: jeconnoc
ms.openlocfilehash: 957ebaa267217d3f4f7981c22062c38382485b74
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865083"
---
# <a name="collect-performance-counters-for-your-azure-cloud-service"></a><span data-ttu-id="f8720-103">Collect performance counters for your Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="f8720-103">Collect performance counters for your Azure Cloud Service</span></span>

<span data-ttu-id="f8720-104">Performance counters provide a way for you to track how well your application and the host are performing.</span><span class="sxs-lookup"><span data-stu-id="f8720-104">Performance counters provide a way for you to track how well your application and the host are performing.</span></span> <span data-ttu-id="f8720-105">Windows Server provides many different performance counters related to hardware, applications, the operating system, and more.</span><span class="sxs-lookup"><span data-stu-id="f8720-105">Windows Server provides many different performance counters related to hardware, applications, the operating system, and more.</span></span> <span data-ttu-id="f8720-106">By collecting and sending performance counters to Azure, you can analyze this information to help make better decisions.</span><span class="sxs-lookup"><span data-stu-id="f8720-106">By collecting and sending performance counters to Azure, you can analyze this information to help make better decisions.</span></span> 

## <a name="discover-available-counters"></a><span data-ttu-id="f8720-107">Discover available counters</span><span class="sxs-lookup"><span data-stu-id="f8720-107">Discover available counters</span></span>

<span data-ttu-id="f8720-108">A performance counter is made up of two parts, a set name (also known as a category) and one or more counters.</span><span class="sxs-lookup"><span data-stu-id="f8720-108">A performance counter is made up of two parts, a set name (also known as a category) and one or more counters.</span></span> <span data-ttu-id="f8720-109">You can use PowerShell to get a list of available performance counters:</span><span class="sxs-lookup"><span data-stu-id="f8720-109">You can use PowerShell to get a list of available performance counters:</span></span>

```PowerShell
Get-Counter -ListSet * | Select-Object CounterSetName, Paths | Sort-Object CounterSetName

CounterSetName                                  Paths
--------------                                  -----
.NET CLR Data                                   {\.NET CLR Data(*)\SqlClient...
.NET CLR Exceptions                             {\.NET CLR Exceptions(*)\# o...
.NET CLR Interop                                {\.NET CLR Interop(*)\# of C...
.NET CLR Jit                                    {\.NET CLR Jit(*)\# of Metho...
.NET Data Provider for Oracle                   {\.NET Data Provider for Ora...
.NET Data Provider for SqlServer                {\.NET Data Provider for Sql...
.NET Memory Cache 4.0                           {\.NET Memory Cache 4.0(*)\C...
AppV Client Streamed Data Percentage            {\AppV Client Streamed Data ...
ASP.NET                                         {\ASP.NET\Application Restar...
ASP.NET Apps v4.0.30319                         {\ASP.NET Apps v4.0.30319(*)...
ASP.NET State Service                           {\ASP.NET State Service\Stat...
ASP.NET v2.0.50727                              {\ASP.NET v2.0.50727\Applica...
ASP.NET v4.0.30319                              {\ASP.NET v4.0.30319\Applica...
Authorization Manager Applications              {\Authorization Manager Appl...

#... results cut to save space ...
```

<span data-ttu-id="f8720-110">The `CounterSetName` property represents a set (or category), and is a good indicator of what the performance counters are related to.</span><span class="sxs-lookup"><span data-stu-id="f8720-110">The `CounterSetName` property represents a set (or category), and is a good indicator of what the performance counters are related to.</span></span> <span data-ttu-id="f8720-111">The `Paths` property represents a collection of counters for a set.</span><span class="sxs-lookup"><span data-stu-id="f8720-111">The `Paths` property represents a collection of counters for a set.</span></span> <span data-ttu-id="f8720-112">You could also get the `Description` property for more information about the counter set.</span><span class="sxs-lookup"><span data-stu-id="f8720-112">You could also get the `Description` property for more information about the counter set.</span></span>

<span data-ttu-id="f8720-113">To get all of the counters for a set, use the `CounterSetName` value and expand the `Paths` collection.</span><span class="sxs-lookup"><span data-stu-id="f8720-113">To get all of the counters for a set, use the `CounterSetName` value and expand the `Paths` collection.</span></span> <span data-ttu-id="f8720-114">Each path item is a counter you can query.</span><span class="sxs-lookup"><span data-stu-id="f8720-114">Each path item is a counter you can query.</span></span> <span data-ttu-id="f8720-115">For example, to get the available counters related to the `Processor` set, expand the `Paths` collection:</span><span class="sxs-lookup"><span data-stu-id="f8720-115">For example, to get the available counters related to the `Processor` set, expand the `Paths` collection:</span></span>

```PowerShell
Get-Counter -ListSet * | Where-Object CounterSetName -eq "Processor" | Select -ExpandProperty Paths

\Processor(*)\% Processor Time
\Processor(*)\% User Time
\Processor(*)\% Privileged Time
\Processor(*)\Interrupts/sec
\Processor(*)\% DPC Time
\Processor(*)\% Interrupt Time
\Processor(*)\DPCs Queued/sec
\Processor(*)\DPC Rate
\Processor(*)\% Idle Time
\Processor(*)\% C1 Time
\Processor(*)\% C2 Time
\Processor(*)\% C3 Time
\Processor(*)\C1 Transitions/sec
\Processor(*)\C2 Transitions/sec
\Processor(*)\C3 Transitions/sec
```

<span data-ttu-id="f8720-116">These individual counter paths can be added to the diagnostics framework your cloud service uses.</span><span class="sxs-lookup"><span data-stu-id="f8720-116">These individual counter paths can be added to the diagnostics framework your cloud service uses.</span></span> <span data-ttu-id="f8720-117">For more information about how a performance counter path is constructed, see [Specifying a Counter Path](https://msdn.microsoft.com/library/windows/desktop/aa373193(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="f8720-117">For more information about how a performance counter path is constructed, see [Specifying a Counter Path](https://msdn.microsoft.com/library/windows/desktop/aa373193(v=vs.85)).</span></span>

## <a name="collect-a-performance-counter"></a><span data-ttu-id="f8720-118">Collect a performance counter</span><span class="sxs-lookup"><span data-stu-id="f8720-118">Collect a performance counter</span></span>

<span data-ttu-id="f8720-119">A performance counter can be added to your cloud service for either Azure Diagnostics or Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f8720-119">A performance counter can be added to your cloud service for either Azure Diagnostics or Application Insights.</span></span>

### <a name="application-insights"></a><span data-ttu-id="f8720-120">Application Insights</span><span class="sxs-lookup"><span data-stu-id="f8720-120">Application Insights</span></span>

<span data-ttu-id="f8720-121">Azure Application Insights for Cloud Services allows you specify what performance counters you want to collect.</span><span class="sxs-lookup"><span data-stu-id="f8720-121">Azure Application Insights for Cloud Services allows you specify what performance counters you want to collect.</span></span> <span data-ttu-id="f8720-122">After you [add Application Insights to your project](../application-insights/app-insights-cloudservices.md#sdk), a config file named **ApplicationInsights.config** is added to your Visual Studio project.</span><span class="sxs-lookup"><span data-stu-id="f8720-122">After you [add Application Insights to your project](../application-insights/app-insights-cloudservices.md#sdk), a config file named **ApplicationInsights.config** is added to your Visual Studio project.</span></span> <span data-ttu-id="f8720-123">This config file defines what type of information Application Insights collects and sends to Azure.</span><span class="sxs-lookup"><span data-stu-id="f8720-123">This config file defines what type of information Application Insights collects and sends to Azure.</span></span>

<span data-ttu-id="f8720-124">Open the **ApplicationInsights.config** file and find the **ApplicationInsights** > **TelemetryModules** element.</span><span class="sxs-lookup"><span data-stu-id="f8720-124">Open the **ApplicationInsights.config** file and find the **ApplicationInsights** > **TelemetryModules** element.</span></span> <span data-ttu-id="f8720-125">Each `<Add>` child-element defines a type of telemetry to collect, along with its configuration.</span><span class="sxs-lookup"><span data-stu-id="f8720-125">Each `<Add>` child-element defines a type of telemetry to collect, along with its configuration.</span></span> <span data-ttu-id="f8720-126">The performance counter telemetry module type is `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector`.</span><span class="sxs-lookup"><span data-stu-id="f8720-126">The performance counter telemetry module type is `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector`.</span></span> <span data-ttu-id="f8720-127">If this element is already defined, do not add it a second time.</span><span class="sxs-lookup"><span data-stu-id="f8720-127">If this element is already defined, do not add it a second time.</span></span> <span data-ttu-id="f8720-128">Each performance counter to collect is defined under a node named `<Counters>`.</span><span class="sxs-lookup"><span data-stu-id="f8720-128">Each performance counter to collect is defined under a node named `<Counters>`.</span></span> <span data-ttu-id="f8720-129">Here is an example that collects drive performance counters:</span><span class="sxs-lookup"><span data-stu-id="f8720-129">Here is an example that collects drive performance counters:</span></span>

```xml
<ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings">

  <TelemetryModules>

    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\LogicalDisk(C:)\Disk Write Bytes/sec" ReportAs="Disk write (C:)" />
        <Add PerformanceCounter="\LogicalDisk(C:)\Disk Read Bytes/sec" ReportAs="Disk read (C:)" />
      </Counters>
    </Add>

  </TelemetryModules>

<!-- ... cut to save space ... -->
```

<span data-ttu-id="f8720-130">Each performance counter is represented as an `<Add>` element under `<Counters>`.</span><span class="sxs-lookup"><span data-stu-id="f8720-130">Each performance counter is represented as an `<Add>` element under `<Counters>`.</span></span> <span data-ttu-id="f8720-131">The `PerformanceCounter` attribute defines which performance counter to collect.</span><span class="sxs-lookup"><span data-stu-id="f8720-131">The `PerformanceCounter` attribute defines which performance counter to collect.</span></span> <span data-ttu-id="f8720-132">The `ReportAs` attribute is the title to display in the Azure portal for the performance counter.</span><span class="sxs-lookup"><span data-stu-id="f8720-132">The `ReportAs` attribute is the title to display in the Azure portal for the performance counter.</span></span> <span data-ttu-id="f8720-133">Any performance counter you collect is put into a category named **Custom** in the portal.</span><span class="sxs-lookup"><span data-stu-id="f8720-133">Any performance counter you collect is put into a category named **Custom** in the portal.</span></span> <span data-ttu-id="f8720-134">Unlike Azure Diagnostics, you cannot set the interval these performance counters are collected and sent to Azure.</span><span class="sxs-lookup"><span data-stu-id="f8720-134">Unlike Azure Diagnostics, you cannot set the interval these performance counters are collected and sent to Azure.</span></span> <span data-ttu-id="f8720-135">With Application Insights, performance counters are collected and sent every minute.</span><span class="sxs-lookup"><span data-stu-id="f8720-135">With Application Insights, performance counters are collected and sent every minute.</span></span> 

<span data-ttu-id="f8720-136">Application Insights automatically collects the following performance counters:</span><span class="sxs-lookup"><span data-stu-id="f8720-136">Application Insights automatically collects the following performance counters:</span></span>

* <span data-ttu-id="f8720-137">\Process(??APP_WIN32_PROC??)\% Processor Time</span><span class="sxs-lookup"><span data-stu-id="f8720-137">\Process(??APP_WIN32_PROC??)\% Processor Time</span></span>
* <span data-ttu-id="f8720-138">\Memory\Available Bytes</span><span class="sxs-lookup"><span data-stu-id="f8720-138">\Memory\Available Bytes</span></span>
* <span data-ttu-id="f8720-139">\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec</span><span class="sxs-lookup"><span data-stu-id="f8720-139">\.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec</span></span>
* <span data-ttu-id="f8720-140">\Process(??APP_WIN32_PROC??)\Private Bytes</span><span class="sxs-lookup"><span data-stu-id="f8720-140">\Process(??APP_WIN32_PROC??)\Private Bytes</span></span>
* <span data-ttu-id="f8720-141">\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec</span><span class="sxs-lookup"><span data-stu-id="f8720-141">\Process(??APP_WIN32_PROC??)\IO Data Bytes/sec</span></span>
* <span data-ttu-id="f8720-142">\Processor(_Total)\% Processor Time</span><span class="sxs-lookup"><span data-stu-id="f8720-142">\Processor(_Total)\% Processor Time</span></span>

<span data-ttu-id="f8720-143">For more information, see [System performance counters in Application Insights](../application-insights/app-insights-performance-counters.md) and [Application Insights for Azure Cloud Services](../application-insights/app-insights-cloudservices.md#performance-counters).</span><span class="sxs-lookup"><span data-stu-id="f8720-143">For more information, see [System performance counters in Application Insights](../application-insights/app-insights-performance-counters.md) and [Application Insights for Azure Cloud Services](../application-insights/app-insights-cloudservices.md#performance-counters).</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="f8720-144">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f8720-144">Azure Diagnostics</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8720-145">While all this data is aggregated into the storage account, the portal does **not** provide a native way to chart the data.</span><span class="sxs-lookup"><span data-stu-id="f8720-145">While all this data is aggregated into the storage account, the portal does **not** provide a native way to chart the data.</span></span> <span data-ttu-id="f8720-146">It is highly recommended that you integrate another diagnostics service, like Application Insights, into your application.</span><span class="sxs-lookup"><span data-stu-id="f8720-146">It is highly recommended that you integrate another diagnostics service, like Application Insights, into your application.</span></span>

<span data-ttu-id="f8720-147">The Azure Diagnostics extension for Cloud Services allows you specify what performance counters you want to collect.</span><span class="sxs-lookup"><span data-stu-id="f8720-147">The Azure Diagnostics extension for Cloud Services allows you specify what performance counters you want to collect.</span></span> <span data-ttu-id="f8720-148">To set up Azure Diagnostics, see [Cloud Service Monitoring Overview](cloud-services-how-to-monitor.md#setup-diagnostics-extension).</span><span class="sxs-lookup"><span data-stu-id="f8720-148">To set up Azure Diagnostics, see [Cloud Service Monitoring Overview](cloud-services-how-to-monitor.md#setup-diagnostics-extension).</span></span>

<span data-ttu-id="f8720-149">The performance counters you want to collect are defined in the **diagnostics.wadcfgx** file.</span><span class="sxs-lookup"><span data-stu-id="f8720-149">The performance counters you want to collect are defined in the **diagnostics.wadcfgx** file.</span></span> <span data-ttu-id="f8720-150">Open this file (it is defined per role) in Visual Studio and find the **DiagnosticsConfiguration** > **PublicConfig** > **WadCfg** > **DiagnosticMonitorConfiguration** > **PerformanceCounters** element.</span><span class="sxs-lookup"><span data-stu-id="f8720-150">Open this file (it is defined per role) in Visual Studio and find the **DiagnosticsConfiguration** > **PublicConfig** > **WadCfg** > **DiagnosticMonitorConfiguration** > **PerformanceCounters** element.</span></span> <span data-ttu-id="f8720-151">Add a new **PerformanceCounterConfiguration** element as a child.</span><span class="sxs-lookup"><span data-stu-id="f8720-151">Add a new **PerformanceCounterConfiguration** element as a child.</span></span> <span data-ttu-id="f8720-152">This element has two attributes: `counterSpecifier` and `sampleRate`.</span><span class="sxs-lookup"><span data-stu-id="f8720-152">This element has two attributes: `counterSpecifier` and `sampleRate`.</span></span> <span data-ttu-id="f8720-153">The `counterSpecifier` attribute defines which system performance counter set (outlined in the previous section) to collect.</span><span class="sxs-lookup"><span data-stu-id="f8720-153">The `counterSpecifier` attribute defines which system performance counter set (outlined in the previous section) to collect.</span></span> <span data-ttu-id="f8720-154">The `sampleRate` value indicates how often that value is polled.</span><span class="sxs-lookup"><span data-stu-id="f8720-154">The `sampleRate` value indicates how often that value is polled.</span></span> <span data-ttu-id="f8720-155">As a whole, all performance counters are transferred to Azure according to the parent `PerformanceCounters` element's `scheduledTransferPeriod` attribute value.</span><span class="sxs-lookup"><span data-stu-id="f8720-155">As a whole, all performance counters are transferred to Azure according to the parent `PerformanceCounters` element's `scheduledTransferPeriod` attribute value.</span></span>

<span data-ttu-id="f8720-156">For more information about the `PerformanceCounters` schema element, see the [Azure Diagnostics Schema](../monitoring-and-diagnostics/azure-diagnostics-schema-1dot3-and-later.md#performancecounters-element).</span><span class="sxs-lookup"><span data-stu-id="f8720-156">For more information about the `PerformanceCounters` schema element, see the [Azure Diagnostics Schema](../monitoring-and-diagnostics/azure-diagnostics-schema-1dot3-and-later.md#performancecounters-element).</span></span>

<span data-ttu-id="f8720-157">The period defined by the `sampleRate` attribute uses the XML duration data type to indicate how often the performance counter is polled.</span><span class="sxs-lookup"><span data-stu-id="f8720-157">The period defined by the `sampleRate` attribute uses the XML duration data type to indicate how often the performance counter is polled.</span></span> <span data-ttu-id="f8720-158">In the example below, the rate is set to `PT3M`, which means `[P]eriod[T]ime[3][M]inutes`: every three minutes.</span><span class="sxs-lookup"><span data-stu-id="f8720-158">In the example below, the rate is set to `PT3M`, which means `[P]eriod[T]ime[3][M]inutes`: every three minutes.</span></span>

<span data-ttu-id="f8720-159">For more information about how the `sampleRate` and `scheduledTransferPeriod` are defined, see the **Duration Data Type** section in the [W3 XML Date and Time Date Types](https://www.w3schools.com/XML/schema_dtypes_date.asp) tutorial.</span><span class="sxs-lookup"><span data-stu-id="f8720-159">For more information about how the `sampleRate` and `scheduledTransferPeriod` are defined, see the **Duration Data Type** section in the [W3 XML Date and Time Date Types](https://www.w3schools.com/XML/schema_dtypes_date.asp) tutorial.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig>
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096">

        <!-- ... cut to save space ... -->

        <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />

          <!-- This is a new perf counter which will track the C: disk read activity in bytes per second, every minute -->
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(C:)\Disk Read Bytes/sec" sampleRate="PT1M" />

        </PerformanceCounters>
      </DiagnosticMonitorConfiguration>
    </WadCfg>
    
    <!-- ... cut to save space ... -->

  </PublicConfig>
</DiagnosticsConfiguration>
```

## <a name="create-a-new-perf-counter"></a><span data-ttu-id="f8720-160">Create a new perf counter</span><span class="sxs-lookup"><span data-stu-id="f8720-160">Create a new perf counter</span></span>

<span data-ttu-id="f8720-161">A new performance counter can be created and used by your code.</span><span class="sxs-lookup"><span data-stu-id="f8720-161">A new performance counter can be created and used by your code.</span></span> <span data-ttu-id="f8720-162">Your code that creates a new performance counter must be running elevated, otherwise it will fail.</span><span class="sxs-lookup"><span data-stu-id="f8720-162">Your code that creates a new performance counter must be running elevated, otherwise it will fail.</span></span> <span data-ttu-id="f8720-163">Your cloud service `OnStart` startup code can create the performance counter, requiring you to run the role in an elevated context.</span><span class="sxs-lookup"><span data-stu-id="f8720-163">Your cloud service `OnStart` startup code can create the performance counter, requiring you to run the role in an elevated context.</span></span> <span data-ttu-id="f8720-164">Or you can create a startup task that runs elevated and creates the performance counter.</span><span class="sxs-lookup"><span data-stu-id="f8720-164">Or you can create a startup task that runs elevated and creates the performance counter.</span></span> <span data-ttu-id="f8720-165">For more information about startup tasks, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span><span class="sxs-lookup"><span data-stu-id="f8720-165">For more information about startup tasks, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>

<span data-ttu-id="f8720-166">To configure your role to run elevated, add a `<Runtime>` element to the [.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span><span class="sxs-lookup"><span data-stu-id="f8720-166">To configure your role to run elevated, add a `<Runtime>` element to the [.csdef](cloud-services-model-and-package.md#servicedefinitioncsdef) file.</span></span>

```xml
<ServiceDefinition name="CloudServiceLoadTesting" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRoleWithSBQueue1" vmsize="Large">

    <!-- ... cut to save space ... -->

    <Runtime executionContext="elevated">
      
    </Runtime>

    <!-- ... cut to save space ... -->

  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="f8720-167">You can create and register a new performance counter with a few lines of code.</span><span class="sxs-lookup"><span data-stu-id="f8720-167">You can create and register a new performance counter with a few lines of code.</span></span> <span data-ttu-id="f8720-168">Use the `System.Diagnostics.PerformanceCounterCategory.Create` method overload that creates both the category and the counter.</span><span class="sxs-lookup"><span data-stu-id="f8720-168">Use the `System.Diagnostics.PerformanceCounterCategory.Create` method overload that creates both the category and the counter.</span></span> <span data-ttu-id="f8720-169">The following code first checks if the category exists, and if missing, creates both the category and the counter.</span><span class="sxs-lookup"><span data-stu-id="f8720-169">The following code first checks if the category exists, and if missing, creates both the category and the counter.</span></span>

```csharp
using System.Diagnostics;
using Microsoft.WindowsAzure;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRoleWithSBQueue1
{
    public class WorkerRole : RoleEntryPoint
    {
        // Perf counter variable representing times service was used.
        private PerformanceCounter counterServiceUsed;

        public override bool OnStart()
        {
            // ... Other startup code here ...

            // Define the cateogry and counter names.
            string perfCounterCatName = "MyService";
            string perfCounterName = "Times Used";

            // Create the counter if needed. Our counter category only has a single counter.
            // Both the category and counter are created in the same method call.
            if (!PerformanceCounterCategory.Exists(perfCounterCatName))
            {
                PerformanceCounterCategory.Create(perfCounterCatName, "Collects information about the cloud service.", 
                                                  PerformanceCounterCategoryType.SingleInstance, 
                                                  perfCounterName, "How many times the cloud service was used.");
            }

            // Get reference to our counter
            counterServiceUsed = new PerformanceCounter(perfCounterCatName, perfCounterName);
            counterServiceUsed.ReadOnly = false;
            
            return base.OnStart();
        }

        // ... cut class code to save space
    }
}
```

<span data-ttu-id="f8720-170">When you want to use the counter, call the `Increment` or `IncrementBy` method.</span><span class="sxs-lookup"><span data-stu-id="f8720-170">When you want to use the counter, call the `Increment` or `IncrementBy` method.</span></span>

```csharp
// Increase the counter by 1
counterServiceUsed.Increment();
```

<span data-ttu-id="f8720-171">Now that your application uses your custom counter, you need to configure Azure Diagnostics or Application Insights to track the counter.</span><span class="sxs-lookup"><span data-stu-id="f8720-171">Now that your application uses your custom counter, you need to configure Azure Diagnostics or Application Insights to track the counter.</span></span>


### <a name="application-insights"></a><span data-ttu-id="f8720-172">Application Insights</span><span class="sxs-lookup"><span data-stu-id="f8720-172">Application Insights</span></span>

<span data-ttu-id="f8720-173">As previously stated, the performance counters for Application Insights are defined in the **ApplicationInsights.config** file.</span><span class="sxs-lookup"><span data-stu-id="f8720-173">As previously stated, the performance counters for Application Insights are defined in the **ApplicationInsights.config** file.</span></span> <span data-ttu-id="f8720-174">Open **ApplicationInsights.config** and find the **ApplicationInsights** > **TelemetryModules** > **Add** > **Counters** element.</span><span class="sxs-lookup"><span data-stu-id="f8720-174">Open **ApplicationInsights.config** and find the **ApplicationInsights** > **TelemetryModules** > **Add** > **Counters** element.</span></span> <span data-ttu-id="f8720-175">Create an `<Add>` child element and set the `PerformanceCounter` attribute to the category and name of the performance counter you created in your code.</span><span class="sxs-lookup"><span data-stu-id="f8720-175">Create an `<Add>` child element and set the `PerformanceCounter` attribute to the category and name of the performance counter you created in your code.</span></span> <span data-ttu-id="f8720-176">Set the `ReportAs` attribute to a friendly name you want to see in the portal.</span><span class="sxs-lookup"><span data-stu-id="f8720-176">Set the `ReportAs` attribute to a friendly name you want to see in the portal.</span></span>

```xml
<ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings">

  <TelemetryModules>

    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <!-- ... cut other perf counters to save space ... -->

        <!-- This new perf counter matches the [category name]\[counter name] defined in your code -->
        <Add PerformanceCounter="\MyService\Times Used" ReportAs="Service used counter" />
      </Counters>
    </Add>

  </TelemetryModules>

<!-- ... cut to save space ... -->
```

### <a name="azure-diagnostics"></a><span data-ttu-id="f8720-177">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="f8720-177">Azure Diagnostics</span></span>

<span data-ttu-id="f8720-178">As previously stated, the performance counters you want to collect are defined in the **diagnostics.wadcfgx** file.</span><span class="sxs-lookup"><span data-stu-id="f8720-178">As previously stated, the performance counters you want to collect are defined in the **diagnostics.wadcfgx** file.</span></span> <span data-ttu-id="f8720-179">Open this file (it is defined per role) in Visual Studio and find the **DiagnosticsConfiguration** > **PublicConfig** > **WadCfg** > **DiagnosticMonitorConfiguration** > **PerformanceCounters** element.</span><span class="sxs-lookup"><span data-stu-id="f8720-179">Open this file (it is defined per role) in Visual Studio and find the **DiagnosticsConfiguration** > **PublicConfig** > **WadCfg** > **DiagnosticMonitorConfiguration** > **PerformanceCounters** element.</span></span> <span data-ttu-id="f8720-180">Add a new **PerformanceCounterConfiguration** element as a child.</span><span class="sxs-lookup"><span data-stu-id="f8720-180">Add a new **PerformanceCounterConfiguration** element as a child.</span></span> <span data-ttu-id="f8720-181">Set the `counterSpecifier` attribute to the category and name of the performance counter you created in your code.</span><span class="sxs-lookup"><span data-stu-id="f8720-181">Set the `counterSpecifier` attribute to the category and name of the performance counter you created in your code.</span></span> 

```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig>
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096">

        <!-- ... cut to save space ... -->

        <PerformanceCounters scheduledTransferPeriod="PT1M">
          <!-- ... cut other perf counters to save space ... -->
          
          <!-- This new perf counter matches the [category name]\[counter name] defined in your code -->
          <PerformanceCounterConfiguration counterSpecifier="\MyService\Times Used" sampleRate="PT1M" />

        </PerformanceCounters>
      </DiagnosticMonitorConfiguration>
    </WadCfg>
    
    <!-- ... cut to save space ... -->

  </PublicConfig>
</DiagnosticsConfiguration>
```

## <a name="more-information"></a><span data-ttu-id="f8720-182">More information</span><span class="sxs-lookup"><span data-stu-id="f8720-182">More information</span></span>

- [<span data-ttu-id="f8720-183">Application Insights for Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="f8720-183">Application Insights for Azure Cloud Services</span></span>](../application-insights/app-insights-cloudservices.md#performance-counters)
- [<span data-ttu-id="f8720-184">System performance counters in Application Insights</span><span class="sxs-lookup"><span data-stu-id="f8720-184">System performance counters in Application Insights</span></span>](../application-insights/app-insights-performance-counters.md)
- <span data-ttu-id="f8720-185">[Specifying a Counter Path](https://msdn.microsoft.com/library/windows/desktop/aa373193(v=vs.85))</span><span class="sxs-lookup"><span data-stu-id="f8720-185">[Specifying a Counter Path](https://msdn.microsoft.com/library/windows/desktop/aa373193(v=vs.85))</span></span>
- [<span data-ttu-id="f8720-186">Azure Diagnostics Schema - Performance Counters</span><span class="sxs-lookup"><span data-stu-id="f8720-186">Azure Diagnostics Schema - Performance Counters</span></span>](../monitoring-and-diagnostics/azure-diagnostics-schema-1dot3-and-later.md#performancecounters-element)