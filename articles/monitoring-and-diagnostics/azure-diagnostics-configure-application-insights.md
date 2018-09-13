---
title: Configure Azure Diagnostics to send data to Application Insights | Microsoft Docs
description: Update the Azure Diagnostics public configuration to send data to Application Insights.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: ''
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 2ad881c840f7e3ca65e105ed9ce095ef71ff75f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556476"
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="81be6-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span><span class="sxs-lookup"><span data-stu-id="81be6-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="81be6-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span><span class="sxs-lookup"><span data-stu-id="81be6-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="81be6-105">Azure diagnostics sends data to Azure Storage tables.</span><span class="sxs-lookup"><span data-stu-id="81be6-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="81be6-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span><span class="sxs-lookup"><span data-stu-id="81be6-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="81be6-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="81be6-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="81be6-108">Diagnostics configuration explained</span><span class="sxs-lookup"><span data-stu-id="81be6-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="81be6-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="81be6-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="81be6-110">Example configuration of a sink for Application Insights:</span><span class="sxs-lookup"><span data-stu-id="81be6-110">Example configuration of a sink for Application Insights:</span></span>

```XML
    <SinksConfig>
        <Sink name="ApplicationInsights">
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
          <Channels>
            <Channel logLevel="Error" name="MyTopDiagData"  />
            <Channel logLevel="Verbose" name="MyLogData"  />
          </Channels>
        </Sink>
      </SinksConfig>
```

- <span data-ttu-id="81be6-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span><span class="sxs-lookup"><span data-stu-id="81be6-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="81be6-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span><span class="sxs-lookup"><span data-stu-id="81be6-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="81be6-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="81be6-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="81be6-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span><span class="sxs-lookup"><span data-stu-id="81be6-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="81be6-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span><span class="sxs-lookup"><span data-stu-id="81be6-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="81be6-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="81be6-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="81be6-117">The **Channels** element contains one or more **Channel** elements.</span><span class="sxs-lookup"><span data-stu-id="81be6-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="81be6-118">The *name* attribute uniquely refers to that channel.</span><span class="sxs-lookup"><span data-stu-id="81be6-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="81be6-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span><span class="sxs-lookup"><span data-stu-id="81be6-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="81be6-120">The available log levels in order of most to least information are:</span><span class="sxs-lookup"><span data-stu-id="81be6-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="81be6-121">Verbose</span><span class="sxs-lookup"><span data-stu-id="81be6-121">Verbose</span></span>
        - <span data-ttu-id="81be6-122">Information</span><span class="sxs-lookup"><span data-stu-id="81be6-122">Information</span></span>
        - <span data-ttu-id="81be6-123">Warning</span><span class="sxs-lookup"><span data-stu-id="81be6-123">Warning</span></span>
        - <span data-ttu-id="81be6-124">Error</span><span class="sxs-lookup"><span data-stu-id="81be6-124">Error</span></span>
        - <span data-ttu-id="81be6-125">Critical</span><span class="sxs-lookup"><span data-stu-id="81be6-125">Critical</span></span>

<span data-ttu-id="81be6-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span><span class="sxs-lookup"><span data-stu-id="81be6-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="81be6-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span><span class="sxs-lookup"><span data-stu-id="81be6-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="81be6-128">The following graphic shows this relationship.</span><span class="sxs-lookup"><span data-stu-id="81be6-128">The following graphic shows this relationship.</span></span>

![Diagnostics Public Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="81be6-130">The following graphic summarizes the configuration values and how they work.</span><span class="sxs-lookup"><span data-stu-id="81be6-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="81be6-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="81be6-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="81be6-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span><span class="sxs-lookup"><span data-stu-id="81be6-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Diagnostics Sinks  Configuration with Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="81be6-134">Complete sink configuration example</span><span class="sxs-lookup"><span data-stu-id="81be6-134">Complete sink configuration example</span></span>
<span data-ttu-id="81be6-135">Here is a complete example of the public configuration file that</span><span class="sxs-lookup"><span data-stu-id="81be6-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="81be6-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span><span class="sxs-lookup"><span data-stu-id="81be6-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="81be6-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span><span class="sxs-lookup"><span data-stu-id="81be6-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="ApplicationInsights.MyLogData/>
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```

<span data-ttu-id="81be6-138">In the previous configuration, the following lines have the following meanings:</span><span class="sxs-lookup"><span data-stu-id="81be6-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="81be6-139">Send all the data that is being collected by Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="81be6-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="81be6-140">Send only error logs to the Application Insights sink</span><span class="sxs-lookup"><span data-stu-id="81be6-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="81be6-141">Send Verbose application logs to Application Insights</span><span class="sxs-lookup"><span data-stu-id="81be6-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```

## <a name="limitations"></a><span data-ttu-id="81be6-142">Limitations</span><span class="sxs-lookup"><span data-stu-id="81be6-142">Limitations</span></span>

- <span data-ttu-id="81be6-143">**Channels only log type and not performance counters.**</span><span class="sxs-lookup"><span data-stu-id="81be6-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="81be6-144">If you specify a channel with a performance counter element, it is ignored.</span><span class="sxs-lookup"><span data-stu-id="81be6-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="81be6-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span><span class="sxs-lookup"><span data-stu-id="81be6-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="81be6-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span><span class="sxs-lookup"><span data-stu-id="81be6-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="81be6-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span><span class="sxs-lookup"><span data-stu-id="81be6-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="81be6-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span><span class="sxs-lookup"><span data-stu-id="81be6-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="81be6-149">For example, anything specified under the *Directories* node.</span><span class="sxs-lookup"><span data-stu-id="81be6-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="81be6-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="81be6-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81be6-151">Next Steps</span><span class="sxs-lookup"><span data-stu-id="81be6-151">Next Steps</span></span>
* <span data-ttu-id="81be6-152">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span><span class="sxs-lookup"><span data-stu-id="81be6-152">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="81be6-153">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span><span class="sxs-lookup"><span data-stu-id="81be6-153">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>


