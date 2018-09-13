---
title: Configure Azure Diagnostics to send data to Application Insights
description: Update the Azure Diagnostics public configuration to send data to Application Insights.
services: azure-monitor
author: rboucher
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 03/19/2016
ms.author: robb
ms.component: diagnostic-extension
ms.openlocfilehash: 3e1f4076c7a90cbb348f31b7b92e745fff79a04f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44787116"
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="53715-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span><span class="sxs-lookup"><span data-stu-id="53715-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="53715-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span><span class="sxs-lookup"><span data-stu-id="53715-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="53715-105">Azure diagnostics sends data to Azure Storage tables.</span><span class="sxs-lookup"><span data-stu-id="53715-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="53715-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span><span class="sxs-lookup"><span data-stu-id="53715-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="53715-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="53715-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="53715-108">Diagnostics configuration explained</span><span class="sxs-lookup"><span data-stu-id="53715-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="53715-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="53715-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="53715-110">Example configuration of a sink for Application Insights:</span><span class="sxs-lookup"><span data-stu-id="53715-110">Example configuration of a sink for Application Insights:</span></span>

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
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="53715-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span><span class="sxs-lookup"><span data-stu-id="53715-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="53715-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span><span class="sxs-lookup"><span data-stu-id="53715-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="53715-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="53715-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="53715-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span><span class="sxs-lookup"><span data-stu-id="53715-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="53715-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span><span class="sxs-lookup"><span data-stu-id="53715-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="53715-116">See [Use Application Insights with Cloud Services](../application-insights/app-insights-cloudservices.md).</span><span class="sxs-lookup"><span data-stu-id="53715-116">See [Use Application Insights with Cloud Services](../application-insights/app-insights-cloudservices.md).</span></span>

- <span data-ttu-id="53715-117">The **Channels** element contains one or more **Channel** elements.</span><span class="sxs-lookup"><span data-stu-id="53715-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="53715-118">The *name* attribute uniquely refers to that channel.</span><span class="sxs-lookup"><span data-stu-id="53715-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="53715-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span><span class="sxs-lookup"><span data-stu-id="53715-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="53715-120">The available log levels in order of most to least information are:</span><span class="sxs-lookup"><span data-stu-id="53715-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="53715-121">Verbose</span><span class="sxs-lookup"><span data-stu-id="53715-121">Verbose</span></span>
        - <span data-ttu-id="53715-122">Information</span><span class="sxs-lookup"><span data-stu-id="53715-122">Information</span></span>
        - <span data-ttu-id="53715-123">Warning</span><span class="sxs-lookup"><span data-stu-id="53715-123">Warning</span></span>
        - <span data-ttu-id="53715-124">Error</span><span class="sxs-lookup"><span data-stu-id="53715-124">Error</span></span>
        - <span data-ttu-id="53715-125">Critical</span><span class="sxs-lookup"><span data-stu-id="53715-125">Critical</span></span>

<span data-ttu-id="53715-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span><span class="sxs-lookup"><span data-stu-id="53715-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="53715-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span><span class="sxs-lookup"><span data-stu-id="53715-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="53715-128">The following graphic shows this relationship.</span><span class="sxs-lookup"><span data-stu-id="53715-128">The following graphic shows this relationship.</span></span>

![Diagnostics Public Configuration](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="53715-130">The following graphic summarizes the configuration values and how they work.</span><span class="sxs-lookup"><span data-stu-id="53715-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="53715-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="53715-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="53715-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span><span class="sxs-lookup"><span data-stu-id="53715-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Diagnostics Sinks  Configuration with Application Insights](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="53715-134">Complete sink configuration example</span><span class="sxs-lookup"><span data-stu-id="53715-134">Complete sink configuration example</span></span>
<span data-ttu-id="53715-135">Here is a complete example of the public configuration file that</span><span class="sxs-lookup"><span data-stu-id="53715-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="53715-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span><span class="sxs-lookup"><span data-stu-id="53715-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="53715-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span><span class="sxs-lookup"><span data-stu-id="53715-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
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
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
                    "sampleRate": "PT3M"
                }
            ]
        },
        "WindowsEventLog": {
            "scheduledTransferPeriod": "PT1M",
            "DataSource": [
                {
                    "name": "Application!*"
                }
            ]
        },
        "Logs": {
            "scheduledTransferPeriod": "PT1M",
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="53715-138">In the previous configuration, the following lines have the following meanings:</span><span class="sxs-lookup"><span data-stu-id="53715-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="53715-139">Send all the data that is being collected by Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="53715-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="53715-140">Send only error logs to the Application Insights sink</span><span class="sxs-lookup"><span data-stu-id="53715-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="53715-141">Send Verbose application logs to Application Insights</span><span class="sxs-lookup"><span data-stu-id="53715-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="53715-142">Limitations</span><span class="sxs-lookup"><span data-stu-id="53715-142">Limitations</span></span>

- <span data-ttu-id="53715-143">**Channels only log type and not performance counters.**</span><span class="sxs-lookup"><span data-stu-id="53715-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="53715-144">If you specify a channel with a performance counter element, it is ignored.</span><span class="sxs-lookup"><span data-stu-id="53715-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="53715-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span><span class="sxs-lookup"><span data-stu-id="53715-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="53715-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span><span class="sxs-lookup"><span data-stu-id="53715-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="53715-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span><span class="sxs-lookup"><span data-stu-id="53715-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="53715-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span><span class="sxs-lookup"><span data-stu-id="53715-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="53715-149">For example, anything specified under the *Directories* node.</span><span class="sxs-lookup"><span data-stu-id="53715-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="53715-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="53715-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53715-151">Next Steps</span><span class="sxs-lookup"><span data-stu-id="53715-151">Next Steps</span></span>
* <span data-ttu-id="53715-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="53715-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="53715-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span><span class="sxs-lookup"><span data-stu-id="53715-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="53715-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span><span class="sxs-lookup"><span data-stu-id="53715-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
