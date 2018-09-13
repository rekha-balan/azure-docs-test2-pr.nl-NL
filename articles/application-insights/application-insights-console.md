---
title: Azure Application Insights for Console Applications | Microsoft Docs
description: Monitor web applications for availability, performance and usage.
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 08/28/2018
ms.reviewer: lmolkova
ms.author: mbullwin
ms.openlocfilehash: 6d161a49b35bbdfedcb27dd91f9f09dcf7ba4133
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857903"
---
# <a name="application-insights-for-net-console-applications"></a><span data-ttu-id="77cc4-103">Application Insights for .NET console applications</span><span class="sxs-lookup"><span data-stu-id="77cc4-103">Application Insights for .NET console applications</span></span>
<span data-ttu-id="77cc4-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance, and usage.</span><span class="sxs-lookup"><span data-stu-id="77cc4-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance, and usage.</span></span>

<span data-ttu-id="77cc4-105">You need a subscription with [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="77cc4-105">You need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="77cc4-106">Sign in with a Microsoft account, which you might have for Windows, Xbox Live, or other Microsoft cloud services.</span><span class="sxs-lookup"><span data-stu-id="77cc4-106">Sign in with a Microsoft account, which you might have for Windows, Xbox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="77cc4-107">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="77cc4-107">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="77cc4-108">Getting started</span><span class="sxs-lookup"><span data-stu-id="77cc4-108">Getting started</span></span>

* <span data-ttu-id="77cc4-109">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="77cc4-109">In the [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="77cc4-110">For application type, choose **General**.</span><span class="sxs-lookup"><span data-stu-id="77cc4-110">For application type, choose **General**.</span></span>
* <span data-ttu-id="77cc4-111">Take a copy of the Instrumentation Key.</span><span class="sxs-lookup"><span data-stu-id="77cc4-111">Take a copy of the Instrumentation Key.</span></span> <span data-ttu-id="77cc4-112">Find the key in the **Essentials** drop-down of the new resource you created.</span><span class="sxs-lookup"><span data-stu-id="77cc4-112">Find the key in the **Essentials** drop-down of the new resource you created.</span></span> 
* <span data-ttu-id="77cc4-113">Install latest [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights) package.</span><span class="sxs-lookup"><span data-stu-id="77cc4-113">Install latest [Microsoft.ApplicationInsights](https://www.nuget.org/packages/Microsoft.ApplicationInsights) package.</span></span>
* <span data-ttu-id="77cc4-114">Set the instrumentation key in your code before tracking any telemetry (or set APPINSIGHTS_INSTRUMENTATIONKEY environment variable).</span><span class="sxs-lookup"><span data-stu-id="77cc4-114">Set the instrumentation key in your code before tracking any telemetry (or set APPINSIGHTS_INSTRUMENTATIONKEY environment variable).</span></span> <span data-ttu-id="77cc4-115">After that, you should be able to manually track telemetry and see it on the Azure portal</span><span class="sxs-lookup"><span data-stu-id="77cc4-115">After that, you should be able to manually track telemetry and see it on the Azure portal</span></span>

```csharp
TelemetryConfiguration.Active.InstrumentationKey = " *your key* ";
var telemetryClient = new TelemetryClient();
telemetryClient.TrackTrace("Hello World!");
```

* <span data-ttu-id="77cc4-116">Install latest version of [Microsoft.ApplicationInsights.DependencyCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) package - it automatically tracks HTTP, SQL, or some other external dependency calls.</span><span class="sxs-lookup"><span data-stu-id="77cc4-116">Install latest version of [Microsoft.ApplicationInsights.DependencyCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) package - it automatically tracks HTTP, SQL, or some other external dependency calls.</span></span>

<span data-ttu-id="77cc4-117">You may initialize and configure Application Insights from the code or using `ApplicationInsights.config` file.</span><span class="sxs-lookup"><span data-stu-id="77cc4-117">You may initialize and configure Application Insights from the code or using `ApplicationInsights.config` file.</span></span> <span data-ttu-id="77cc4-118">Make sure initialization happens as early as possible.</span><span class="sxs-lookup"><span data-stu-id="77cc4-118">Make sure initialization happens as early as possible.</span></span> 

> [!NOTE]
> <span data-ttu-id="77cc4-119">Instructions referring to **ApplicationInsights.config** are only applicable to apps that are targeting the .NET Framework, and do not apply to .NET Core applications.</span><span class="sxs-lookup"><span data-stu-id="77cc4-119">Instructions referring to **ApplicationInsights.config** are only applicable to apps that are targeting the .NET Framework, and do not apply to .NET Core applications.</span></span>

### <a name="using-config-file"></a><span data-ttu-id="77cc4-120">Using config file</span><span class="sxs-lookup"><span data-stu-id="77cc4-120">Using config file</span></span>

<span data-ttu-id="77cc4-121">By default, Application Insights SDK looks for `ApplicationInsights.config` file in the working directory when `TelemetryConfiguration` is being created</span><span class="sxs-lookup"><span data-stu-id="77cc4-121">By default, Application Insights SDK looks for `ApplicationInsights.config` file in the working directory when `TelemetryConfiguration` is being created</span></span>

```csharp
TelemetryConfiguration config = TelemetryConfiguration.Active; // Reads ApplicationInsights.config file if present
```

<span data-ttu-id="77cc4-122">You may also specify path to the config file.</span><span class="sxs-lookup"><span data-stu-id="77cc4-122">You may also specify path to the config file.</span></span>

```csharp
using System.IO;
TelemetryConfiguration configuration = TelemetryConfiguration.CreateFromConfiguration(File.ReadAllText("C:\\ApplicationInsights.config"));
var telemetryClient = new TelemetryClient(configuration);
```

<span data-ttu-id="77cc4-123">For more information, see [configuration file reference](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="77cc4-123">For more information, see [configuration file reference](app-insights-configuration-with-applicationinsights-config.md).</span></span>

<span data-ttu-id="77cc4-124">You may get a full example of the config file by installing latest version of [Microsoft.ApplicationInsights.WindowsServer](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer) package.</span><span class="sxs-lookup"><span data-stu-id="77cc4-124">You may get a full example of the config file by installing latest version of [Microsoft.ApplicationInsights.WindowsServer](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer) package.</span></span> <span data-ttu-id="77cc4-125">Here is the **minimal** configuration for dependency collection that is equivalent to the code example.</span><span class="sxs-lookup"><span data-stu-id="77cc4-125">Here is the **minimal** configuration for dependency collection that is equivalent to the code example.</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings">
  <InstrumentationKey>Your Key</InstrumentationKey>
  <TelemetryInitializers>
    <Add Type="Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer, Microsoft.AI.DependencyCollector"/>
  </TelemetryInitializers>
  <TelemetryModules>
    <Add Type="Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule, Microsoft.AI.DependencyCollector">
      <ExcludeComponentCorrelationHttpHeadersOnDomains>
        <Add>core.windows.net</Add>
        <Add>core.chinacloudapi.cn</Add>
        <Add>core.cloudapi.de</Add>
        <Add>core.usgovcloudapi.net</Add>
        <Add>localhost</Add>
        <Add>127.0.0.1</Add>
      </ExcludeComponentCorrelationHttpHeadersOnDomains>
      <IncludeDiagnosticSourceActivities>
        <Add>Microsoft.Azure.ServiceBus</Add>
        <Add>Microsoft.Azure.EventHubs</Add>
      </IncludeDiagnosticSourceActivities>
    </Add>
  </TelemetryModules>
  <TelemetryChannel Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel, Microsoft.AI.ServerTelemetryChannel"/>
</ApplicationInsights>

```

### <a name="configuring-telemetry-collection-from-code"></a><span data-ttu-id="77cc4-126">Configuring telemetry collection from code</span><span class="sxs-lookup"><span data-stu-id="77cc4-126">Configuring telemetry collection from code</span></span>

* <span data-ttu-id="77cc4-127">During application start-up create and configure `DependencyTrackingTelemetryModule` instance - it must be singleton and must be preserved for application lifetime.</span><span class="sxs-lookup"><span data-stu-id="77cc4-127">During application start-up create and configure `DependencyTrackingTelemetryModule` instance - it must be singleton and must be preserved for application lifetime.</span></span>

```csharp
var module = new DependencyTrackingTelemetryModule();

// prevent Correlation Id to be sent to certain endpoints. You may add other domains as needed.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
//...

// enable known dependency tracking, note that in future versions, we will extend this list. 
// please check default settings in https://github.com/Microsoft/ApplicationInsights-dotnet-server/blob/develop/Src/DependencyCollector/NuGet/ApplicationInsights.config.install.xdt#L20
module.IncludeDiagnosticSourceActivities.Add("Microsoft.Azure.ServiceBus");
module.IncludeDiagnosticSourceActivities.Add("Microsoft.Azure.EventHubs");
//....

// initialize the module
module.Initialize(configuration);
```

* <span data-ttu-id="77cc4-128">Add common telemetry initializers</span><span class="sxs-lookup"><span data-stu-id="77cc4-128">Add common telemetry initializers</span></span>

```csharp
// stamps telemetry with correlation identifiers
TelemetryConfiguration.Active.TelemetryInitializers.Add(new OperationCorrelationTelemetryInitializer());

// ensures proper DependencyTelemetry.Type is set for Azure RESTful API calls
TelemetryConfiguration.Active.TelemetryInitializers.Add(new HttpDependenciesParsingTelemetryInitializer());
```

* <span data-ttu-id="77cc4-129">For .NET Framework Windows app, you may also install and initialize Performance Counter collector module as described [here](http://apmtips.com/blog/2017/02/13/enable-application-insights-live-metrics-from-code/)</span><span class="sxs-lookup"><span data-stu-id="77cc4-129">For .NET Framework Windows app, you may also install and initialize Performance Counter collector module as described [here](http://apmtips.com/blog/2017/02/13/enable-application-insights-live-metrics-from-code/)</span></span>

#### <a name="full-example"></a><span data-ttu-id="77cc4-130">Full example</span><span class="sxs-lookup"><span data-stu-id="77cc4-130">Full example</span></span>

```csharp
using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DependencyCollector;
using Microsoft.ApplicationInsights.Extensibility;
using System.Net.Http;
using System.Threading.Tasks;

namespace ConsoleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            TelemetryConfiguration configuration = TelemetryConfiguration.Active;

            configuration.InstrumentationKey = "removed";
            configuration.TelemetryInitializers.Add(new OperationCorrelationTelemetryInitializer());
            configuration.TelemetryInitializers.Add(new HttpDependenciesParsingTelemetryInitializer());

            var telemetryClient = new TelemetryClient();
            using (InitializeDependencyTracking(configuration))
            {
                // run app...

                telemetryClient.TrackTrace("Hello World!");

                using (var httpClient = new HttpClient())
                {
                    // Http dependency is automatically tracked!
                    httpClient.GetAsync("https://microsoft.com").Wait();
                }

            }

            // before exit, flush the remaining data
            telemetryClient.Flush();

            // flush is not blocking so wait a bit
            Task.Delay(5000).Wait();

        }

        static DependencyTrackingTelemetryModule InitializeDependencyTracking(TelemetryConfiguration configuration)
        {
            var module = new DependencyTrackingTelemetryModule();

            // prevent Correlation Id to be sent to certain endpoints. You may add other domains as needed.
            module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
            module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.chinacloudapi.cn");
            module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.cloudapi.de");
            module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.usgovcloudapi.net");
            module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("localhost");
            module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("127.0.0.1");

            // enable known dependency tracking, note that in future versions, we will extend this list. 
            // please check default settings in https://github.com/Microsoft/ApplicationInsights-dotnet-server/blob/develop/Src/DependencyCollector/NuGet/ApplicationInsights.config.install.xdt#L20
            module.IncludeDiagnosticSourceActivities.Add("Microsoft.Azure.ServiceBus");
            module.IncludeDiagnosticSourceActivities.Add("Microsoft.Azure.EventHubs");

            // initialize the module
            module.Initialize(configuration);

            return module;
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="77cc4-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="77cc4-131">Next steps</span></span>
* <span data-ttu-id="77cc4-132">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL, or other external resources are slowing you down.</span><span class="sxs-lookup"><span data-stu-id="77cc4-132">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL, or other external resources are slowing you down.</span></span>
* <span data-ttu-id="77cc4-133">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span><span class="sxs-lookup"><span data-stu-id="77cc4-133">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
